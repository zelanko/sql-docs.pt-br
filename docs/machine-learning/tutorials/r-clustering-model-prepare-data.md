---
title: 'Tutorial: Preparar dados para executar o clustering no R'
titleSuffix: SQL machine learning
description: Na parte dois desta série de tutoriais de quatro partes, você preparará os dados de um banco de dados para executar clustering no R com o machine learning do SQL.
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.reviewer: garye, davidph
ms.date: 05/21/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 1c6bf16d51d0180b56007f237001d01cedfecf8d
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870266"
---
# <a name="tutorial-prepare-data-to-perform-clustering-in-r-with-sql-machine-learning"></a>Tutorial: preparar dados para executar clustering no R com o aprendizado de máquina do SQL
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Na parte dois desta série de tutoriais de quatro partes, você preparará os dados de um banco de dados para executar clustering no R com os Serviços de Machine Learning do SQL Server ou em Clusters de Big Data.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Na parte dois desta série de tutoriais de quatro partes, você preparará os dados de um banco de dados para executar clustering no R com os Serviços de Machine Learning do SQL Server.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Na parte dois desta série de tutoriais de quatro partes, você preparará os dados de um banco de dados para executar clustering no R com o SQL Server 2016 R Services.
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
Na parte dois desta série de tutoriais de quatro partes, você preparará os dados de um banco de dados para executar clustering no R com os Serviços de Machine Learning da Instância Gerenciada de SQL do Azure.
::: moniker-end

Neste artigo, você aprenderá a:

> [!div class="checklist"]
> * Clientes separados em dimensões diferentes usando o R
> * Carregar os dados do banco de dados em uma estrutura de dados do R

Na [parte um](r-clustering-model-introduction.md), você instalou os pré-requisitos e restaurou o banco de dados de exemplo.

Na [parte três](r-clustering-model-build.md), você aprenderá a criar e treinar um modelo de cluster K-means no R.

Na [parte quatro](r-clustering-model-deploy.md), você aprenderá a criar um procedimento armazenado em um banco de dados que possa executar clustering no R com base em novos dados.

## <a name="prerequisites"></a>Pré-requisitos

* A parte dois deste tutorial pressupõe que você concluiu a [**parte um**](r-clustering-model-introduction.md).

## <a name="separate-customers"></a>Separar os clientes

Crie um novo arquivo RScript no RStudio e execute o script a seguir.
Na consulta SQL, você está separando clientes nas seguintes dimensões:

* **orderRatio** = taxa de devolução de pedidos (número total de pedidos parcialmente ou totalmente retornados em relação o número total de pedidos)
* **itemsRatio** = taxa de devolução de itens (número total de itens retornados em relação ao número de itens comprados)
* **monetaryRatio** = taxa de valores devolvidos (valor monetário total dos itens retornados em relação ao valor comprado)
* **frequência** = frequência de devoluções

Na função **connStr**, substitua **ServerName** por suas informações de conexão.

```r
# Define the connection string to connect to the tpcxbb_1gb database

connStr <- "Driver=SQL Server;Server=ServerName;Database=tpcxbb_1gb;uid=Username;pwd=Password"

#Define the query to select data
input_query <- "
SELECT ss_customer_sk AS customer
    ,round(CASE 
            WHEN (
                       (orders_count = 0)
                    OR (returns_count IS NULL)
                    OR (orders_count IS NULL)
                    OR ((returns_count / orders_count) IS NULL)
                    )
                THEN 0.0
            ELSE (cast(returns_count AS NCHAR(10)) / orders_count)
            END, 7) AS orderRatio
    ,round(CASE 
            WHEN (
                     (orders_items = 0)
                  OR (returns_items IS NULL)
                  OR (orders_items IS NULL)
                  OR ((returns_items / orders_items) IS NULL)
                 )
            THEN 0.0
            ELSE (cast(returns_items AS NCHAR(10)) / orders_items)
            END, 7) AS itemsRatio
    ,round(CASE 
            WHEN (
                     (orders_money = 0)
                  OR (returns_money IS NULL)
                  OR (orders_money IS NULL)
                  OR ((returns_money / orders_money) IS NULL)
                 )
            THEN 0.0
            ELSE (cast(returns_money AS NCHAR(10)) / orders_money)
            END, 7) AS monetaryRatio
    ,round(CASE 
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
    ) returned ON ss_customer_sk = sr_customer_sk";
```

## <a name="load-the-data-into-a-data-frame"></a>Carregar os dados em um quadro de dados

Agora, use o script a seguir para retornar os resultados da consulta para uma estrutura de dados do R.

```r
# Query using input_query and get the results back
# to data frame customer_data

library(RODBC)

ch <- odbcDriverConnect(connStr)

customer_data <- sqlQuery(ch, input_query)

# Take a look at the data just loaded
head(customer_data, n = 5);
```

Você deverá ver resultados semelhantes aos seguintes.

```results
  customer orderRatio itemsRatio monetaryRatio frequency
1    29727          0          0      0.000000         0
2    26429          0          0      0.041979         1
3    60053          0          0      0.065762         3
4    97643          0          0      0.037034         3
5    32549          0          0      0.031281         4
```

## <a name="clean-up-resources"></a>Limpar os recursos

Se você não continuar com este tutorial, exclua o banco de dados tpcxbb_1gb.

## <a name="next-steps"></a>Próximas etapas

Na parte dois desta série de tutoriais, você aprendeu a:

* Clientes separados em dimensões diferentes usando o R
* Carregar os dados do banco de dados em uma estrutura de dados do R

Para criar um modelo de machine learning que usa esses dados do cliente, siga a parte três desta série de tutoriais:

> [!div class="nextstepaction"]
> [Criar um modelo preditivo no R com o aprendizado de máquina do SQL](r-clustering-model-build.md)
