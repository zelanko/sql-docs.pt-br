---
title: 'Tutorial: Preparar dados para categorizar os clientes em Python'
description: Na parte dois desta série de tutoriais de quatro partes, você preparará os dados de um banco de dado SQL Server para executar o clustering em Python com SQL Server Serviços de Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/30/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d91f3b9f1e3d1abe53d677d9f9058058d321d985
ms.sourcegitcommit: 26715b4dbef95d99abf2ab7198a00e6e2c550243
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70294341"
---
# <a name="tutorial-prepare-data-to-categorize-customers-in-python-with-sql-server-machine-learning-services"></a>Tutorial: Preparar dados para categorizar clientes em Python com SQL Server Serviços de Machine Learning

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Na parte dois desta série de tutoriais de quatro partes, você irá restaurar e preparar os dados de um banco de dados SQL usando o Python. Posteriormente nesta série, você usará esses dados para treinar e implantar um modelo de clustering em Python com SQL Server Serviços de Machine Learning.

Neste artigo, você aprenderá a:

> [!div class="checklist"]
> * Separar clientes ao longo de dimensões diferentes usando o Python
> * Carregar os dados do banco de dados SQL em um quadro de dado do Python

Na [parte um](python-clustering-model.md), você instalou os pré-requisitos e restaurou o banco de dados de exemplo.

Na [terceira parte](python-clustering-model-build.md), você aprenderá a criar e treinar um modelo de clustering K-means em Python.

Na [parte quatro](python-clustering-model-deploy.md), você aprenderá a criar um procedimento armazenado em um banco de dados SQL que pode executar o clustering em Python com base em novas informações.

## <a name="prerequisites"></a>Pré-requisitos

* A parte dois deste tutorial pressupõe que você atende aos pré-requisitos da [**parte 1**](python-clustering-model.md).

## <a name="separate-customers"></a>Clientes separados

Para se preparar para os clientes de clustering, você primeiro separará clientes ao longo das seguintes dimensões:

* **orderRatio** = taxa de ordem de retorno (número total de pedidos parcialmente ou totalmente retornados versus o número total de pedidos)
* **itemsRatio** = taxa de itens de retorno (número total de itens retornados versus o número de itens comprados)
* **monetaryRatio** = taxa de valor de retorno (valor monetário total de itens retornados versus o valor comprado)
* **frequência** = frequência de retorno

Abra um novo bloco de anotações em Azure Data Studio e insira o script a seguir.

Na cadeia de conexão, substitua os detalhes da conexão conforme necessário.

```python
# Load packages.
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import revoscalepy as revoscale
from scipy.spatial import distance as sci_distance
from sklearn import cluster as sk_cluster

################################################################################################

## Connect to DB and select data

################################################################################################

# Connection string to connect to SQL Server named instance.
conn_str = 'Driver=SQL Server;Server=localhost;Database=tpcxbb_1gb;Trusted_Connection=True;'

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

Os resultados da consulta são retornados para o Python usando a função revoscalepy **RxSqlServerData** . Como parte do processo, você usará as informações de coluna definidas no script anterior.

```python
data_source = revoscale.RxSqlServerData(sql_query=input_query, column_Info=column_info,
                                        connection_string=conn_str)
revoscale.RxInSqlServer(connection_string=conn_str, num_tasks=1, auto_cleanup=False)
# import data source and convert to pandas dataframe.
customer_data = pd.DataFrame(revoscale.rx_import(data_source))
```

Agora, exiba o início do quadro de dados para verificar se ele parece correto.

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

## <a name="clean-up-resources"></a>Limpar recursos

Se você não for continuar com este tutorial, exclua o banco de dados tpcxbb_1gb de SQL Server.

## <a name="next-steps"></a>Próximas etapas

Na parte dois desta série de tutoriais, você concluiu estas etapas:

* Separar clientes ao longo de dimensões diferentes usando o Python
* Carregar os dados do banco de dados SQL em um quadro de dado do Python

Para criar um modelo de aprendizado de máquina que usa esses dados do cliente, siga a parte três desta série de tutoriais:

> [!div class="nextstepaction"]
> [Tutorial: Criar um modelo de previsão em Python com SQL Server Serviços de Machine Learning](python-clustering-model-build.md)
