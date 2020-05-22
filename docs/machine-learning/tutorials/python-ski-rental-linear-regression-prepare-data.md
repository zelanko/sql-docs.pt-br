---
title: 'Tutorial do Python: Preparar dados'
titleSuffix: SQL machine learning
description: Na parte dois desta série de tutoriais de quatro partes, você usará o Python para preparar dados a fim de prever aluguéis de esqui com o aprendizado de máquina do SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 75f475f8a2b4b0d23d95498a69f5e5d745f7510d
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606718"
---
# <a name="python-tutorial-prepare-data-to-train-a-linear-regression-model-with-sql-machine-learning"></a>Tutorial do Python: Preparar dados para treinar um modelo de regressão linear com o aprendizado de máquina do SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Na parte dois desta série de tutoriais de quatro partes, você preparará os dados de um banco de dados usando o Python. Posteriormente nesta série, você usará esses dados para treinar e implantar um modelo de regressão linear em Python com os Serviços de Machine Learning do SQL Server ou nos Clusters de Big Data.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Na parte dois desta série de tutoriais de quatro partes, você preparará os dados de um banco de dados usando o Python. Posteriormente nesta série, você usará esses dados para treinar e implantar um modelo de regressão linear em Python com os Serviços de Machine Learning do SQL Server.
::: moniker-end

Neste artigo, você aprenderá a:

> [!div class="checklist"]
> * Carregar os dados do banco de dados do SQL Server em uma estrutura de dados do **Pandas**
> * Preparar os dados no Python removendo algumas colunas

Na [parte um](python-ski-rental-linear-regression.md), você aprendeu a restaurar o banco de dados de exemplo.

Na [parte três](python-ski-rental-linear-regression-train-model.md), você aprenderá a treinar um modelo de machine learning de regressão linear no Python.

Na [parte quatro](python-ski-rental-linear-regression-deploy-model.md), você aprenderá a armazenar o modelo em um banco de dados e, em seguida, criará procedimentos armazenados com base nos scripts do Python desenvolvidos nas partes dois e três. Os procedimentos armazenados serão executados no servidor para fazer previsões com base em novos dados.

## <a name="prerequisites"></a>Pré-requisitos

* A parte dois deste tutorial pressupõe que você concluiu a [parte um](python-ski-rental-linear-regression.md) e os respectivos pré-requisitos.

## <a name="explore-and-prepare-the-data"></a>Explorar e preparar os dados

Para usar os dados no Python, você os carregará do banco de dados em uma estrutura do Pandas.

Crie um notebook do Python no Azure Data Studio e execute o script abaixo. Substitua `<SQL Server>` pelo seu próprio nome do SQL Server.

O script Python abaixo importa o conjunto de dados da tabela **dbo.rental_data** em seu banco de dados para uma estrutura de dados **df** do Pandas.

Na cadeia de conexão, substitua os detalhes da conexão conforme necessário.

```python
import pyodbc
import pandas
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error

# Connection string to your SQL Server instance
conn_str = pyodbc.connect('DRIVER={ODBC Driver 17 for SQL Server}; SERVER=<SQL Server>; DATABASE=TutorialDB; Trusted_Connection=yes')

query_str = 'SELECT Year, Month, Day, Rentalcount, Weekday, Holiday, Snow FROM dbo.rental_data'

df = pandas.read_sql(sql=query_str, con=conn_str)

print("Data frame:", df)

# Get all the columns from the dataframe.
columns = df.columns.tolist()

# Filter the columns to remove ones we don't want to use in the training
columns = [c for c in columns if c not in ["Year"]]
```

Você deverá ver resultados semelhantes aos seguintes.

```results
Data frame:      Year  Month  Day  RentalCount  WeekDay  Holiday  Snow
0    2014      1   20          445        2        1     0
1    2014      2   13           40        5        0     0
2    2013      3   10          456        1        0     0
3    2014      3   31           38        2        0     0
4    2014      4   24           23        5        0     0
..    ...    ...  ...          ...      ...      ...   ...
448  2013      2   19           57        3        0     1
449  2015      3   18           26        4        0     0
450  2015      3   24           29        3        0     1
451  2014      3   26           50        4        0     1
452  2015     12    6          377        1        0     1

[453 rows x 7 columns]
```

## <a name="next-steps"></a>Próximas etapas

Na parte dois desta série de tutoriais, você concluiu estas etapas:

* Carregar os dados do banco de dados em uma estrutura do **Pandas**
* Preparar os dados no Python removendo algumas colunas

Para treinar um modelo de machine learning que usa dados do banco de dados TutorialDB, siga a parte três desta série de tutoriais:

> [!div class="nextstepaction"]
> [Tutorial do Python: Treinar um modelo de regressão linear](python-ski-rental-linear-regression-train-model.md)