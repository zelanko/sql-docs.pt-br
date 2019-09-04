---
title: 'Tutorial do Python: Preparar dados (regressão linear)'
description: Neste tutorial, você usará a regressão linear e Python em SQL Server Serviços de Machine Learning para prever o número de locações de esqui. Você preparará os dados de um banco de dado SQL Server usando Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c6c4d5fb4ffc5049f7e1325267b7623dc195e9d8
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70242494"
---
# <a name="python-tutorial-prepare-data-to-train-a-linear-regression-model-in-sql-server-machine-learning-services"></a>Tutorial do Python: Preparar dados para treinar um modelo de regressão linear no SQL Server Serviços de Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Na parte dois desta série de tutoriais de quatro partes, você preparará os dados de um SQL Server o uso do Python. Posteriormente nesta série, você usará esses dados para treinar e implantar um modelo de regressão linear em Python com SQL Server Serviços de Machine Learning.

Neste artigo, você aprenderá a:

> [!div class="checklist"]
> * Carregar os dados do banco de dados do SQL Server em um quadro do data pandas
> * Preparar os dados no Python removendo algumas colunas

Na [parte um](python-ski-rental-linear-regression.md), você aprendeu a restaurar o banco de dados de exemplo.

Na [terceira parte](python-ski-rental-linear-regression-train-model.md), você aprenderá a treinar um modelo de aprendizado de máquina de regressão linear no Python.

Na [parte quatro](python-ski-rental-linear-regression-deploy-model.md), você aprenderá a armazenar o modelo para SQL Server e, em seguida, criar procedimentos armazenados a partir dos scripts Python desenvolvidos nas partes dois e três. Os procedimentos armazenados serão executados no SQL Server para fazer previsões com base em novos dados.

## <a name="prerequisites"></a>Pré-requisitos

* A parte dois deste tutorial pressupõe que você concluiu a [parte um](python-ski-rental-linear-regression.md) e seus pré-requisitos.

## <a name="explore-and-prepare-the-data"></a>Explorar e preparar os dados

Para usar os dados no Python, você carregará os dados do banco de dados do SQL Server em um quadro de dados do pandas.

Crie um novo bloco de anotações do Python no Azure Data Studio e execute o script a seguir. Substitua `<SQL Server>` pelo seu próprio nome de SQL Server.

O script do Python abaixo importa o conjunto de dados da tabela **dbo. rental_data** em seu Database para um data frame do pandas **DF**.

```python
import pandas as pd
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from revoscalepy import RxComputeContext, RxInSqlServer, RxSqlServerData
from revoscalepy import rx_import

# Connection string to your SQL Server instance
conn_str = 'Driver=SQL Server;Server=<SQL Server>;Database=TutorialDB;Trusted_Connection=True;'

# Define the columns you will import
 column_info = {
         "Year" : { "type" : "integer" },
         "Month" : { "type" : "integer" },
         "Day" : { "type" : "integer" },
         "RentalCount" : { "type" : "integer" },
         "WeekDay" : {
             "type" : "factor",
             "levels" : ["1", "2", "3", "4", "5", "6", "7"]
         },
         "Holiday" : {
             "type" : "factor",
             "levels" : ["1", "0"]
         },
         "Snow" : {
             "type" : "factor",
             "levels" : ["1", "0"]
         }
     }

# Get the data from the SQL Server table
data_source = RxSqlServerData(table="dbo.rental_data",
                               connection_string=conn_str, column_info=column_info)
computeContext = RxInSqlServer(
     connection_string = conn_str,
     num_tasks = 1,
     auto_cleanup = False
)

RxInSqlServer(connection_string=conn_str, num_tasks=1, auto_cleanup=False)

# import data source and convert to pandas dataframe
df = pd.DataFrame(rx_import(input_data = data_source))
print("Data frame:", df)

# Get all the columns from the dataframe.
columns = df.columns.tolist()

# Filter the columns to remove ones we don't want to use in the training
columns = [c for c in columns if c not in ["Year"]]
```

Você deverá ver resultados semelhantes ao seguinte.

```results
Rows Processed: 453
Data frame:      Day  Holiday  Month  RentalCount  Snow  WeekDay  Year
0     20        1      1          445     2        2  2014
1     13        2      2           40     2        5  2014
2     10        2      3          456     2        1  2013
3     31        2      3           38     2        2  2014
4     24        2      4           23     2        5  2014
5     11        2      2           42     2        4  2015
6     28        2      4          310     2        1  2013
...
[453 rows x 7 columns]
```

## <a name="next-steps"></a>Próximas etapas

Na parte dois desta série de tutoriais, você concluiu estas etapas:

* Carregar os dados do banco de dados do SQL Server em um quadro do data pandas
* Preparar os dados no Python removendo algumas colunas

Para treinar um modelo de aprendizado de máquina que usa dados do banco de TutorialDB, siga a parte três desta série de tutoriais:

> [!div class="nextstepaction"]
> [Tutorial do Python: Treinar um modelo de regressão linear](python-ski-rental-linear-regression-train-model.md)