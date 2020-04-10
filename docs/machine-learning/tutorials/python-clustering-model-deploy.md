---
title: 'Tutorial do Python: implantar um modelo de cluster'
description: Na parte quatro desta série de tutoriais de quatro partes, você implantará um modelo de clustering em Python com os Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/27/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: df0fd7cb27977679a6ca879d7ae01045ed3fa8c8
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116559"
---
# <a name="tutorial-deploy-a-model-in-python-to-categorize-customers-with-sql-server-machine-learning-services"></a>Tutorial: Implantar um modelo em Python para categorizar clientes com os Serviços de Machine Learning do SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Na parte quatro desta série de tutoriais de quatro partes, você implantará um modelo de clustering, desenvolvido em Python em um Banco de Dados SQL usando os Serviços de Machine Learning do SQL Server.

Para executar o clustering regularmente, à medida que novos clientes se registram, você precisa ser capaz de chamar o script Python de qualquer aplicativo. Para fazer isso, você pode implantar o script Python no SQL Server colocando-o dentro de um procedimento armazenado do SQL no banco de dados. Como seu modelo é executado no Banco de Dados SQL, ele pode ser facilmente treinado em relação aos dados armazenados no banco de dados.

Nesta seção, você moverá o código Python que acabou de escrever no SQL Server e implantará o clustering com a ajuda dos Serviços de Machine Learning do SQL Server.

Neste artigo, você aprenderá a:

> [!div class="checklist"]
> * Criar o procedimento armazenado que gera o modelo
> * Executar clustering no SQL Server
> * Usar as informações de clustering

Na [parte um](python-clustering-model.md), você instalou os pré-requisitos e restaurou o banco de dados de exemplo.

Na [parte dois](python-clustering-model-prepare-data.md), você aprendeu a preparar os dados de um Banco de Dados SQL para executar o clustering.

Na [parte três](python-clustering-model-build.md), você aprendeu a criar e treinar um modelo de clustering K-means em Python.

## <a name="prerequisites"></a>Pré-requisitos

* A parte quatro desta série de tutoriais pressupõe que você cumpriu os pré-requisitos da [**parte um**](python-clustering-model.md)e concluiu as etapas na [**parte dois**](python-clustering-model-prepare-data.md) e na [**parte três**](python-clustering-model-build.md).

## <a name="create-a-stored-procedure-that-generates-the-model"></a>Criar o procedimento armazenado que gera o modelo

Execute o seguinte script T-SQL para criar o procedimento armazenado. O procedimento recria as etapas que você desenvolveu na primeira e na segunda parte desta série de tutoriais:

* classificar clientes com base em seu histórico de compras e devoluções e
* gerar quatro clusters de clientes usando um algoritmo K-means

```sql
USE [tpcxbb_1gb]
GO

CREATE procedure [dbo].[py_generate_customer_return_clusters]
AS

BEGIN
    DECLARE

-- Input query to generate the purchase history & return metrics
     @input_query NVARCHAR(MAX) = N'
SELECT
  ss_customer_sk AS customer,
  CAST( (ROUND(COALESCE(returns_count / NULLIF(1.0*orders_count, 0), 0), 7) ) AS FLOAT) AS orderRatio,
  CAST( (ROUND(COALESCE(returns_items / NULLIF(1.0*orders_items, 0), 0), 7) ) AS FLOAT) AS itemsRatio,
  CAST( (ROUND(COALESCE(returns_money / NULLIF(1.0*orders_money, 0), 0), 7) ) AS FLOAT) AS monetaryRatio,
  CAST( (COALESCE(returns_count, 0)) AS FLOAT) AS frequency
FROM
  (
    SELECT
      ss_customer_sk,
      -- return order ratio
      COUNT(distinct(ss_ticket_number)) AS orders_count,
      -- return ss_item_sk ratio
      COUNT(ss_item_sk) AS orders_items,
      -- return monetary amount ratio
      SUM( ss_net_paid ) AS orders_money
    FROM store_sales s
    GROUP BY ss_customer_sk
  ) orders
  LEFT OUTER JOIN
  (
    SELECT
      sr_customer_sk,
      -- return order ratio
      count(distinct(sr_ticket_number)) as returns_count,
      -- return ss_item_sk ratio
      COUNT(sr_item_sk) as returns_items,
      -- return monetary amount ratio
      SUM( sr_return_amt ) AS returns_money
    FROM store_returns
    GROUP BY sr_customer_sk
  ) returned ON ss_customer_sk=sr_customer_sk
 '

EXEC sp_execute_external_script
      @language = N'Python'
    , @script = N'

import pandas as pd
from sklearn.cluster import KMeans

#get data from input query
customer_data = my_input_data

#We concluded in step 2 in the tutorial that 4 would be a good number of clusters
n_clusters = 4

#Perform clustering
est = KMeans(n_clusters=n_clusters, random_state=111).fit(customer_data[["orderRatio","itemsRatio","monetaryRatio","frequency"]])
clusters = est.labels_
customer_data["cluster"] = clusters

OutputDataSet = customer_data
'
    , @input_data_1 = @input_query
    , @input_data_1_name = N'my_input_data'
             with result sets (("Customer" int, "orderRatio" float,"itemsRatio" float,"monetaryRatio" float,"frequency" float,"cluster" float));
END;
GO
```

## <a name="perform-clustering-in-sql-database"></a>Executar clustering no Banco de Dados SQL

Agora que você criou o procedimento armazenado, execute o script a seguir para realizar o clustering usando o procedimento.

```sql
--Create a table to store the predictions in

DROP TABLE IF EXISTS [dbo].[py_customer_clusters];
GO

CREATE TABLE [dbo].[py_customer_clusters] (
    [Customer] [bigint] NULL
  , [OrderRatio] [float] NULL
  , [itemsRatio] [float] NULL
  , [monetaryRatio] [float] NULL
  , [frequency] [float] NULL
  , [cluster] [int] NULL
  ,
    ) ON [PRIMARY]
GO

--Execute the clustering and insert results into table
INSERT INTO py_customer_clusters
EXEC [dbo].[py_generate_customer_return_clusters];

-- Select contents of the table to verify it works
SELECT * FROM py_customer_clusters;
```

## <a name="use-the-clustering-information"></a>Usar as informações de clustering

Como você armazenou o procedimento de clustering no banco de dados, ele pode realizar o clustering com eficiência em relação aos dados do cliente armazenados no mesmo banco de dados. Você pode executar o procedimento sempre que os dados do cliente são atualizados e usar as informações de clustering atualizadas.

Imagine que você deseja enviar um email promocional aos clientes no cluster 0, o grupo que estava inativo (você pode ver como os quatro clusters foram descritos na [parte três](python-clustering-model-build.md#analyze-the-results) deste tutorial). O código a seguir seleciona os endereços de email dos clientes no cluster 0.

```sql
USE [tpcxbb_1gb]
--Get email addresses of customers in cluster 0 for a promotion campaign
SELECT customer.[c_email_address], customer.c_customer_sk
  FROM dbo.customer
  JOIN
  [dbo].[py_customer_clusters] as c
  ON c.Customer = customer.c_customer_sk
  WHERE c.cluster = 0
```

É possível alterar o valor **c.cluster** para retornar endereços de email de clientes de outros clusters.

## <a name="clean-up-resources"></a>Limpar os recursos

Após concluir este tutorial, você poderá excluir o banco de dados do tpcxbb_1gb do SQL Server.

## <a name="next-steps"></a>Próximas etapas

Na parte quatro desta série de tutoriais, você concluiu estas etapas:

* Criar o procedimento armazenado que gera o modelo
* Executar clustering no SQL Server
* Usar as informações de clustering

Para saber mais sobre como usar o Python nos Serviços de Machine Learning do SQL Server, confira:

* [Início Rápido: Criar e executar scripts Python simples com os Serviços de Machine Learning do SQL Server](quickstart-python-create-script.md)
* [Outros tutoriais do Python para os Serviços de Machine Learning do SQL Server](sql-server-python-tutorials.md)
* [Instalar pacotes Python com o sqlmlutils](../package-management/install-additional-python-packages-on-sql-server.md)

