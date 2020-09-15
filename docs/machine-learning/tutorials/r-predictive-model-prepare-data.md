---
title: 'Tutorial: Preparar os dados para treinar um modelo preditivo no R'
titleSuffix: SQL machine learning
description: Na parte dois desta série de tutoriais de quatro partes, você preparará os dados para treinar um modelo preditivo no R com o aprendizado de máquina do SQL.
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: cawrites
ms.author: chadam
ms.reviewer: garye, davidph
ms.date: 05/21/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 0be451ea14a6eec98872b3c21b16c5065d02f85f
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178716"
---
# <a name="tutorial-prepare-data-to-train-a-predictive-model-in-r-with-sql-machine-learning"></a>Tutorial: preparar os dados para treinar um modelo preditivo no R com o aprendizado de máquina do SQL
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Na parte dois deste tutorial de quatro partes, você preparará os dados de um banco de dados usando o R. Ainda nesta série, você usará esses dados para treinar e implantar um modelo preditivo em R com os Serviços de Machine Learning do SQL Server ou nos Clusters de Big Data.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Na parte dois deste tutorial de quatro partes, você preparará os dados de um banco de dados usando o R. Ainda nesta série, você usará esses dados para treinar e implantar um modelo preditivo em R com os Serviços de Machine Learning do SQL Server.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Na parte dois deste tutorial de quatro partes, você preparará os dados de um banco de dados usando o R. Ainda nesta série, você usará esses dados para treinar e implantar um modelo preditivo em R com o SQL Server R Services.
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
Na parte dois deste tutorial de quatro partes, você preparará os dados de um banco de dados usando o R. Ainda nesta série, você usará esses dados para treinar e implantar um modelo preditivo em R com os Serviços de Machine Learning da Instância Gerenciada de SQL do Azure.
::: moniker-end

Neste artigo, você aprenderá a:

> [!div class="checklist"]
> * Restaurar um banco de dados de exemplo em um banco de dados
> * Carregar os dados do banco de dados em uma estrutura de dados do R
> * Preparar os dados no R identificando algumas colunas como categóricas

Na [parte um](r-predictive-model-introduction.md), você aprendeu a restaurar o banco de dados de exemplo.

Na [parte três](r-predictive-model-train.md), você aprenderá a treinar um modelo de machine learning no R.

Na [parte quatro](r-predictive-model-deploy.md), você aprenderá a armazenar o modelo em um banco de dados e, em seguida, criará procedimentos armazenados com base nos scripts do R desenvolvidos nas partes dois e três. Os procedimentos armazenados serão executados no servidor para fazer previsões com base em novos dados.

## <a name="prerequisites"></a>Pré-requisitos

A parte dois deste tutorial presume que você concluiu a [**parte um**](r-predictive-model-introduction.md) e seus pré-requisitos.

## <a name="load-the-data-into-a-data-frame"></a>Carregar os dados em um quadro de dados

Para usar os dados no R, é necessário carregá-los do banco de dados para a estrutura de dados (`rentaldata`).

Crie um novo arquivo RScript no RStudio e execute o script a seguir. Substitua **ServerName** por suas informações de conexão.

```r
#Define the connection string to connect to the TutorialDB database
connStr <- "Driver=SQL Server;Server=ServerName;Database=TutorialDB;uid=Username;pwd=Password"


#Get the data from the table
library(RODBC)

ch <- odbcDriverConnect(connStr)

#Import the data from the table
rentaldata <- sqlFetch(ch, "dbo.rental_data")

#Take a look at the structure of the data and the top rows
head(rentaldata)
str(rentaldata)
```

Você deverá ver resultados semelhantes aos seguintes.

```results
   Year  Month  Day  RentalCount  WeekDay  Holiday  Snow
1  2014    1     20      445         2        1      0
2  2014    2     13       40         5        0      0
3  2013    3     10      456         1        0      0
4  2014    3     31       38         2        0      0
5  2014    4     24       23         5        0      0
6  2015    2     11       42         4        0      0
'data.frame':       453 obs. of  7 variables:
$ Year       : int  2014 2014 2013 2014 2014 2015 2013 2014 2013 2015 ...
$ Month      : num  1 2 3 3 4 2 4 3 4 3 ...
$ Day        : num  20 13 10 31 24 11 28 8 5 29 ...
$ RentalCount: num  445 40 456 38 23 42 310 240 22 360 ...
$ WeekDay    : num  2 5 1 2 5 4 1 7 6 1 ...
$ Holiday    : int  1 0 0 0 0 0 0 0 0 0 ...
$ Snow       : num  0 0 0 0 0 0 0 0 0 0 ...
```

## <a name="prepare-the-data"></a>Preparar os dados

Neste banco de dados de exemplo, a maior parte da preparação já foi feita, mas você fará uma preparação a mais.
Use o seguinte script do R para identificar as três colunas como *categorias* alterando os tipos de dados para *fator*.



```r
#Changing the three factor columns to factor types
rentaldata$Holiday <- factor(rentaldata$Holiday);
rentaldata$Snow    <- factor(rentaldata$Snow);
rentaldata$WeekDay <- factor(rentaldata$WeekDay);



#Visualize the dataset after the change
str(rentaldata);
```

Você deverá ver resultados semelhantes aos seguintes.

```results
data.frame':      453 obs. of  7 variables:
$ Year       : int  2014 2014 2013 2014 2014 2015 2013 2014 2013 2015 ...
$ Month      : num  1 2 3 3 4 2 4 3 4 3 ...
$ Day        : num  20 13 10 31 24 11 28 8 5 29 ...
$ RentalCount: num  445 40 456 38 23 42 310 240 22 360 ...
$ WeekDay    : Factor w/ 7 levels "1","2","3","4",..: 2 5 1 2 5 4 1 7 6 1 ...
$ Holiday    : Factor w/ 2 levels "0","1": 2 1 1 1 1 1 1 1 1 1 ...
$ Snow       : Factor w/ 2 levels "0","1": 1 1 1 1 1 1 1 1 1 1 ...
```

Os dados agora estão preparados para treinamento.

## <a name="clean-up-resources"></a>Limpar os recursos

Se você não continuar com este tutorial, exclua o banco de dados TutorialDB.

## <a name="next-steps"></a>Próximas etapas

Na parte dois desta série de tutoriais, você aprendeu a:

* Carregar os dados de exemplo em uma estrutura de dados do R
* Preparar os dados no R identificando algumas colunas como categóricas

Para criar um modelo de machine learning que usa dados do banco de dados TutorialDB, siga a parte três desta série de tutoriais:

> [!div class="nextstepaction"]
> [Criar um modelo preditivo no R com o aprendizado de máquina do SQL](r-predictive-model-train.md)
