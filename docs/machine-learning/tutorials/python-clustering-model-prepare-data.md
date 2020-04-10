---
title: 'Tutorial do Python: preparar dados do cluster'
description: Na parte dois desta série de tutoriais de quatro partes, você preparará os dados do SQL para executarem clustering em Python com os Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 12/17/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8ee19ddfa59f8f1a4a32c0adf08b8f36eef9aa1f
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116509"
---
# <a name="tutorial-prepare-data-to-categorize-customers-in-python-with-sql-server-machine-learning-services"></a>Tutorial: Preparar dados para categorizar clientes em Python com os Serviços de Machine Learning do SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Na parte dois desta série de tutoriais de quatro partes, você restaurará e preparará os dados de um Banco de Dados SQL usando o Python. Posteriormente nesta série, você usará esses dados para treinar e implantar um modelo de clustering em Python com os Serviços de Machine Learning do SQL Server.

Neste artigo, você aprenderá a:

> [!div class="checklist"]
> * Separar clientes ao longo de dimensões diferentes usando o Python
> * Carregar os dados do Banco de Dados SQL em um quadro de dados do Python

Na [parte um](python-clustering-model.md), você instalou os pré-requisitos e restaurou o banco de dados de exemplo.

Na [parte três](python-clustering-model-build.md), você aprenderá a criar e treinar um modelo de cluster K-means em Python.

Na [parte quatro](python-clustering-model-deploy.md), você aprenderá a criar um procedimento armazenado em um Banco de Dados SQL que pode executar clusters em Python com base em novos dados.

## <a name="prerequisites"></a>Pré-requisitos

* A parte dois deste tutorial pressupõe que você cumpriu os pré-requisitos da [**parte um**](python-clustering-model.md).

## <a name="separate-customers"></a>Separar os clientes

Para se preparar para os clientes de clustering, primeiro você separará os clientes ao longo das seguintes dimensões:

* **orderRatio** = taxa de devolução de pedidos (número total de pedidos parcialmente ou totalmente retornados em relação o número total de pedidos)
* **itemsRatio** = taxa de devolução de itens (número total de itens retornados em relação ao número de itens comprados)
* **monetaryRatio** = taxa de valores devolvidos (valor monetário total dos itens retornados em relação ao valor comprado)
* **frequência** = frequência de devoluções

Abra um novo notebook no Azure Data Studio e insira o script a seguir.

Na cadeia de conexão, substitua os detalhes da conexão conforme necessário.

```python
# Load packages.
import pyodbc
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
from scipy.spatial import distance as sci_distance
from sklearn import cluster as sk_cluster

################################################################################################

## Connect to DB and select data

################################################################################################

# Connection string to connect to SQL Server named instance.
conn_str = pyodbc.connect('DRIVER={ODBC Driver 17 for SQL Server}; SERVER=localhost; DATABASE=tpcxbb_1gb; Trusted_Connection=yes')

input_query = '''SELECT
ss_customer_sk AS customer,
ROUND(COALESCE(returns_count / NULLIF(1.0*orders_count, 0), 0), 7) AS orderRatio,
ROUND(COALESCE(returns_items / NULLIF(1.0*orders_items, 0), 0), 7) AS itemsRatio,
ROUND(COALESCE(returns_money / NULLIF(1.0*orders_money, 0), 0), 7) AS monetaryRatio,
COALESCE(returns_count, 0) AS frequency
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
GROUP BY sr_customer_sk ) returned ON ss_customer_sk=sr_customer_sk'''


# Define the columns we wish to import.
column_info = {
    "customer": {"type": "integer"},
    "orderRatio": {"type": "integer"},
    "itemsRatio": {"type": "integer"},
    "frequency": {"type": "integer"}
}
```

## <a name="load-the-data-into-a-data-frame"></a>Carregar os dados em um quadro de dados

Os resultados da consulta são retornados para o Python usando a função **read_sql** do Pandas. Como parte do processo, você usará as informações de coluna definidas no script anterior.

```python
customer_data = pandas.read_sql(input_query, conn_str)
```

Agora, exiba o início do quadro de dados para verificar se ela parece correta.

```python
print("Data frame:", customer_data.head(n=5))
```

```results
Rows Read: 37336, Total Rows Processed: 37336, Total Chunk Time: 0.172 seconds
Data frame:     customer  orderRatio  itemsRatio  monetaryRatio  frequency
0    29727.0    0.000000    0.000000       0.000000          0
1    97643.0    0.068182    0.078176       0.037034          3
2    57247.0    0.000000    0.000000       0.000000          0
3    32549.0    0.086957    0.068657       0.031281          4
4     2040.0    0.000000    0.000000       0.000000          0
```

## <a name="clean-up-resources"></a>Limpar os recursos

Se você não continuar com este tutorial, exclua o banco de dados tpcxbb_1gb do SQL Server.

## <a name="next-steps"></a>Próximas etapas

Na parte dois desta série de tutoriais, você concluiu estas etapas:

* Separar clientes ao longo de dimensões diferentes usando o Python
* Carregar os dados do Banco de Dados SQL em um quadro de dados do Python

Para criar um modelo de machine learning que usa esses dados do cliente, siga a parte três desta série de tutoriais:

> [!div class="nextstepaction"]
> [Tutorial: Criar um modelo de previsão em Python com os Serviços de Machine Learning do SQL Server](python-clustering-model-build.md)
