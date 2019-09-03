---
title: 'Tutorial: Implantar um modelo de clustering em Python'
description: Na parte quatro desta série de tutoriais de quatro partes, você implantará um modelo de clustering em Python com SQL Server Serviços de Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/27/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 746629d35be93997e4cda389e284aee9bb5f8544
ms.sourcegitcommit: 3de1fb410de2515e5a00a5dbf6dd442d888713ba
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2019
ms.locfileid: "70211930"
---
# <a name="tutorial-deploy-a-clustering-model-in-python-with-sql-server-machine-learning-services"></a>Tutorial: Implantar um modelo de clustering em Python com SQL Server Serviços de Machine Learning

Na parte quatro desta série de tutoriais de quatro partes, você implantará um modelo de clustering, desenvolvido em Python, em um banco de dados SQL usando SQL Server Serviços de Machine Learning.

Para executar o cluster regularmente, à medida que novos clientes estão se registrando, você precisa ser capaz de chamar o script Python de qualquer aplicativo. Para fazer isso, você pode implantar o script Python no SQL Server colocando o script Python dentro de um procedimento armazenado do SQL no banco de dados. Como seu modelo é executado no banco de dados SQL, ele pode ser facilmente treinado em relação aos dados armazenados no banco de dado.

Nesta seção, você moverá o código Python que acabou de escrever em SQL Server e implantará o clustering com a ajuda de SQL Server Serviços de Machine Learning.

Neste artigo, você aprenderá a:

> [!div class="checklist"]
> * Criar um procedimento armazenado que gera o modelo
> * Executar clustering no SQL Server
> * Usar as informações de clustering

Na [parte um](tutorial-python-clustering-model.md), você instalou os pré-requisitos e importou o banco de dados de exemplo.

Na [parte dois](tutorial-python-clustering-model-prepare-data.md), você aprendeu como preparar os dados de um banco de dado SQL para executar o clustering.

Na [terceira parte](tutorial-python-clustering-model-build.md), você aprendeu a criar e treinar um modelo de clustering K-means em Python.

## <a name="prerequisites"></a>Pré-requisitos

* A parte quatro desta série de tutoriais pressupõe que você atendeu aos pré-requisitos da [**parte 1**](tutorial-python-clustering-model.md)e concluiu as etapas na parte [**dois**](tutorial-python-clustering-model-prepare-data.md) e na [**parte três**](tutorial-python-clustering-model-build.md).

## <a name="create-a-stored-procedure-that-generates-the-model"></a>Criar um procedimento armazenado que gera o modelo

Execute o seguinte script T-SQL para criar o procedimento armazenado. O procedimento recria as etapas que você desenvolveu nas partes um e duas desta série de tutoriais:

* classificar clientes com base em seu histórico de compras e de retorno
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

## <a name="perform-clustering-in-sql-database"></a>Executar clustering no banco de dados SQL

Agora que você criou o procedimento armazenado, execute o script a seguir para executar o Clustering usando o procedimento.

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

Como você armazenou o procedimento de clustering no banco de dados, ele pode realizar o clustering com eficiência em relação ao cliente armazenado no mesmo banco de dado. Você pode executar o procedimento sempre que os dados do cliente são atualizados e usar as informações de clustering atualizadas.

Suponha que você deseja enviar um email promocional aos clientes no cluster 0, o grupo que estava inativo (você pode ver como os quatro clusters foram descritos na [parte três](tutorial-python-clustering-model-build.md#analyze-the-results) deste tutorial). O código a seguir seleciona os endereços de email de clientes no cluster 0.

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

Você pode alterar o valor de **cluster c** para retornar endereços de email para clientes em outros clusters.

## <a name="clean-up-resources"></a>Limpar recursos

Quando tiver concluído este tutorial, você poderá excluir o banco de dados tpcxbb_1gb de SQL Server.

## <a name="next-steps"></a>Próximas etapas

Na parte quatro desta série de tutoriais, você concluiu estas etapas:

* Criar um procedimento armazenado que gera o modelo
* Executar clustering no SQL Server
* Usar as informações de clustering

Para saber mais sobre como usar o Python no Serviços de Machine Learning SQL Server, confira:

* [Início Rápido: Execute um script Python "Olá, mundo" em SQL Server Serviços de Machine Learning](quickstart-python-run-using-t-sql.md)
* [Outros tutoriais do Python para SQL Server Serviços de Machine Learning](sql-server-python-tutorials.md)
* [Instalar pacotes do Python com o sqlmlutils](../package-management/install-additional-python-packages-on-sql-server.md)

