---
title: 'Tutorial: Implantar um modelo de clustering no R'
titleSuffix: SQL machine learning
description: Na parte quatro desta série de tutoriais de quatro partes, você implantará um modelo de clustering no R com o aprendizado de máquina do SQL.
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: cawrites
ms.author: chadam
ms.reviewer: garye, davidph
ms.date: 05/21/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 327038528ddc238eb5644ad8c0c4b35e2b969313
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178443"
---
# <a name="tutorial-deploy-a-clustering-model-in-r-with-sql-machine-learning"></a>Tutorial: Implantar um modelo de clustering no R com o aprendizado de máquina do SQL
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Na parte quatro desta série de tutoriais de quatro partes, você implantará um modelo de clustering, desenvolvido em R, em um banco de dados usando os Serviços de Machine Learning do SQL Server ou nos Clusters de Big Data.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Na parte quatro desta série de tutoriais de quatro partes, você implantará um modelo de clustering, desenvolvido em R, em um banco de dados usando os Serviços de Machine Learning do SQL Server.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Na parte quatro desta série de tutoriais de quatro partes, você implantará um modelo de clustering, desenvolvido em R, em um banco de dados usando o SQL Server R Services.
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
Na parte quatro desta série de tutoriais de quatro partes, você implantará um modelo de clustering, desenvolvido em R, em um banco de dados usando os Serviços de Machine Learning da Instância Gerenciada de SQL do Azure.
::: moniker-end

Para executar o clustering regularmente, à medida que novos clientes se registrarem, você precisará ser capaz de chamar o script do R em qualquer aplicativo. Para fazer isso, você pode implantar o script do R em um banco de dados colocando-o dentro de um procedimento armazenado do SQL. Como seu modelo é executado no banco de dados, ele pode ser facilmente treinado em relação aos dados armazenados no banco de dados.

Neste artigo, você aprenderá a:

> [!div class="checklist"]
> * Criar o procedimento armazenado que gera o modelo
> * Executar clustering
> * Usar as informações de clustering

Na [parte um](r-clustering-model-introduction.md), você instalou os pré-requisitos e restaurou o banco de dados de exemplo.

Na [parte dois](r-clustering-model-prepare-data.md), você aprendeu a preparar os dados de um banco de dados para executar clustering.

Na [parte três](r-clustering-model-build.md), você aprendeu a criar e treinar um modelo de cluster K-means no R.

## <a name="prerequisites"></a>Pré-requisitos

* A parte quatro desta série de tutoriais pressupõe que você cumpriu os pré-requisitos da [**parte um**](r-clustering-model-introduction.md) e concluiu as etapas na [**parte dois**](r-clustering-model-build.md) e na [**parte três**](r-clustering-model-build.md).

## <a name="create-a-stored-procedure-that-generates-the-model"></a>Criar o procedimento armazenado que gera o modelo

Execute o seguinte script T-SQL para criar o procedimento armazenado. O procedimento recria as etapas que você desenvolveu nas partes dois e três desta série de tutoriais:

* classificar clientes com base em seu histórico de compras e devoluções e
* gerar quatro clusters de clientes usando um algoritmo K-means

O procedimento armazena os mapeamentos de cluster do cliente resultantes na tabela de banco de dados **customer_return_clusters**.

```sql
USE [tpcxbb_1gb]
DROP PROC IF EXISTS generate_customer_return_clusters;
GO
CREATE procedure [dbo].[generate_customer_return_clusters]
AS
/*
  This procedure uses R to classify customers into different groups
  based on their purchase & return history.
*/
BEGIN
    DECLARE @duration FLOAT
    , @instance_name NVARCHAR(100) = @@SERVERNAME
    , @database_name NVARCHAR(128) = db_name()
-- Input query to generate the purchase history & return metrics
    , @input_query NVARCHAR(MAX) = N'
SELECT ss_customer_sk AS customer,
    round(CASE 
            WHEN (
                    (orders_count = 0)
                    OR (returns_count IS NULL)
                    OR (orders_count IS NULL)
                    OR ((returns_count / orders_count) IS NULL)
                    )
                THEN 0.0
            ELSE (cast(returns_count AS NCHAR(10)) / orders_count)
            END, 7) AS orderRatio,
    round(CASE 
            WHEN (
                    (orders_items = 0)
                    OR (returns_items IS NULL)
                    OR (orders_items IS NULL)
                    OR ((returns_items / orders_items) IS NULL)
                    )
                THEN 0.0
            ELSE (cast(returns_items AS NCHAR(10)) / orders_items)
            END, 7) AS itemsRatio,
    round(CASE 
            WHEN (
                    (orders_money = 0)
                    OR (returns_money IS NULL)
                    OR (orders_money IS NULL)
                    OR ((returns_money / orders_money) IS NULL)
                    )
                THEN 0.0
            ELSE (cast(returns_money AS NCHAR(10)) / orders_money)
            END, 7) AS monetaryRatio,
    round(CASE 
            WHEN (returns_count IS NULL)
                THEN 0.0
            ELSE returns_count
            END, 0) AS frequency
FROM (
    SELECT ss_customer_sk,
        -- return order ratio
        COUNT(DISTINCT (ss_ticket_number)) AS orders_count,
        -- return ss_item_sk ratio
        COUNT(ss_item_sk) AS orders_items,
        -- return monetary amount ratio
        SUM(ss_net_paid) AS orders_money
    FROM store_sales s
    GROUP BY ss_customer_sk
    ) orders
LEFT OUTER JOIN (
    SELECT sr_customer_sk,
        -- return order ratio
        count(DISTINCT (sr_ticket_number)) AS returns_count,
        -- return ss_item_sk ratio
        COUNT(sr_item_sk) AS returns_items,
        -- return monetary amount ratio
        SUM(sr_return_amt) AS returns_money
    FROM store_returns
    GROUP BY sr_customer_sk
    ) returned ON ss_customer_sk = sr_customer_sk
 '
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
# Define the connection string

connStr <- paste("Driver=SQL Server; Server=", instance_name,
                 "; Database=", database_name,
                 "; uid=Username;pwd=Password; ",
                 sep="" )

# Input customer data that needs to be classified.
# This is the result we get from the query.
library(RODBC)

ch <- odbcDriverConnect(connStr);

customer_data <- sqlQuery(ch, input_query)

sqlDrop(ch, "customer_return_clusters")

## create clustering model
clust <- kmeans(customer_data[,2:5],4)

## create clustering output for table
customer_cluster <- data.frame(cluster=clust$cluster,customer=customer_data$customer,orderRatio=customer_data$orderRatio,
            itemsRatio=customer_data$itemsRatio,monetaryRatio=customer_data$monetaryRatio,frequency=customer_data$frequency)

## write cluster output to DB table
sqlSave(ch, customer_cluster, tablename = "customer_return_clusters")

## clean up
odbcClose(ch)
'
    , @input_data_1 = N''
    , @params = N'@instance_name nvarchar(100), @database_name nvarchar(128), @input_query nvarchar(max), @duration float OUTPUT'
    , @instance_name = @instance_name
    , @database_name = @database_name
    , @input_query = @input_query
    , @duration = @duration OUTPUT;
END;

GO
```

## <a name="perform-clustering"></a>Executar clustering

Agora que você criou o procedimento armazenado, execute o script a seguir para executar o clustering.

```sql
--Empty table of the results before running the stored procedure
TRUNCATE TABLE customer_return_clusters;

--Execute the clustering
--This will load the table customer_return_clusters with cluster mappings
EXECUTE [dbo].[generate_customer_return_clusters];
```

Verifique se ele funciona e se, de fato, temos a lista de clientes e seus mapeamentos de cluster.

```sql
--Select data from table customer_return_clusters
--to verify that the clustering data was loaded
SELECT TOP (5) *
FROM customer_return_clusters;
```

```result
cluster  customer  orderRatio  itemsRatio  monetaryRatio  frequency
1        29727     0           0           0              0
4        26429     0           0           0.041979       1
2        60053     0           0           0.065762       3
2        97643     0           0           0.037034       3
2        32549     0           0           0.031281       4
```

## <a name="use-the-clustering-information"></a>Usar as informações de clustering

Como você armazenou o procedimento de clustering no banco de dados, ele pode realizar o clustering com eficiência em relação aos dados do cliente armazenados no mesmo banco de dados. Você pode executar o procedimento sempre que os dados do cliente são atualizados e usar as informações de clustering atualizadas.

Imagine que você deseja enviar um email promocional aos clientes no cluster 0, o grupo que estava inativo (você pode ver como os quatro clusters foram descritos na [parte três](r-clustering-model-build.md#analyze-the-results) deste tutorial). O código a seguir seleciona os endereços de email dos clientes no cluster 0.

```sql
USE [tpcxbb_1gb]
--Get email addresses of customers in cluster 0 for a promotion campaign
SELECT customer.[c_email_address], customer.c_customer_sk
  FROM dbo.customer
  JOIN
  [dbo].[customer_clusters] as c
  ON c.Customer = customer.c_customer_sk
  WHERE c.cluster = 0
```

É possível alterar o valor **c.cluster** para retornar endereços de email de clientes de outros clusters.

## <a name="clean-up-resources"></a>Limpar os recursos

Após concluir este tutorial, você poderá excluir o banco de dados do tpcxbb_1gb.

## <a name="next-steps"></a>Próximas etapas

Na parte quatro desta série de tutoriais, você aprendeu a:

* Criar o procedimento armazenado que gera o modelo
* Executar clustering com o machine learning do SQL
* Usar as informações de clustering

Para saber mais sobre como usar o R nos Serviços de Machine Learning, confira:

* [Executar scripts simples do R](quickstart-r-create-script.md)
* [Estruturas, tipos e objetos de dados do R](quickstart-r-data-types-and-objects.md)
* [Funções do R](quickstart-r-functions.md)
