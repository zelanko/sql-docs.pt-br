---
title: 'Tutorial: Implantar um modelo preditivo no R'
titleSuffix: SQL machine learning
description: Na parte quatro desta série de tutoriais de quatro partes, você implantará um modelo preditivo no R com o aprendizado de máquina do SQL.
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.reviewer: garye, davidph
ms.date: 05/21/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current'
ms.openlocfilehash: bc5cb5f0b5a79b7e9ff81171e0a1b7b31ad580db
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470157"
---
# <a name="tutorial-deploy-a-predictive-model-in-r-with-sql-machine-learning"></a>Tutorial: implantar um modelo preditivo no R com o aprendizado de máquina do SQL
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
Na parte quatro desta série de tutoriais de quatro partes, você implantará um modelo de machine learning desenvolvido em R nos Serviços de Machine Learning do SQL Server ou em Clusters de Big Data.
::: moniker-end
::: moniker range="=sql-server-2017"
Na parte quatro desta série de tutoriais de quatro partes, você implantará um modelo de machine learning, desenvolvido em R, em um banco de dados SQL usando os Serviços de Machine Learning do SQL Server.
::: moniker-end
::: moniker range="=sql-server-2016"
Na parte quatro desta série de tutoriais de quatro partes, você implantará um modelo de machine learning, desenvolvido em R, no SQL Server usando o SQL Server R Services.
::: moniker-end
::: moniker range="=azuresqldb-mi-current"
Na parte quatro desta série de tutoriais de quatro partes, você implantará um modelo de machine learning desenvolvido em R na Instância Gerenciada de SQL do Azure usando Serviços de Machine Learning.
::: moniker-end

Neste artigo, você aprenderá a:

> [!div class="checklist"]
> * Criar um procedimento armazenado que gera o modelo de machine learning
> * Armazenar o modelo em uma tabela de banco de dados
> * Criar um procedimento armazenado que faça previsões usando o modelo
> * Executar o modelo com novos dados

Na [parte um](r-predictive-model-introduction.md), você aprendeu a restaurar o banco de dados de exemplo.

Na [parte dois](r-predictive-model-prepare-data.md), você aprendeu a importar um banco de dados de exemplo e, em seguida, preparar os dados para serem usados no treinamento de um modelo preditivo em R.

Na [parte três](r-predictive-model-train.md), você aprendeu a criar e treinar vários modelos de machine learning em R e, em seguida, escolheu o mais preciso.

## <a name="prerequisites"></a>Pré-requisitos

A parte quatro deste tutorial pressupõe que você cumpriu os pré-requisitos da [**parte um**](r-predictive-model-introduction.md) e concluiu as etapas na [**parte dois**](r-predictive-model-prepare-data.md) e na [**parte três**](r-predictive-model-train.md).

## <a name="create-a-stored-procedure-that-generates-the-model"></a>Criar o procedimento armazenado que gera o modelo

Na parte três desta série de tutoriais, você decidiu que um modelo de árvore de decisão (dtree) era o mais preciso. Agora, com os scripts de R desenvolvidos, crie um procedimento armazenado (`generate_rental_model`) que treina e gera o modelo de dtree usando rpart do pacote R.

Execute os comandos a seguir no Azure Data Studio.

```sql
USE [TutorialDB]
DROP PROCEDURE IF EXISTS generate_rental_model;
GO
CREATE PROCEDURE generate_rental_model (@trained_model VARBINARY(max) OUTPUT)
AS
BEGIN
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
rental_train_data$Month   <- factor(rental_train_data$Month);
rental_train_data$Day     <- factor(rental_train_data$Day);
rental_train_data$Holiday <- factor(rental_train_data$Holiday);
rental_train_data$Snow    <- factor(rental_train_data$Snow);
rental_train_data$WeekDay <- factor(rental_train_data$WeekDay);

#Create a dtree model and train it using the training data set
library(rpart);
model_dtree <- rpart(RentalCount ~ Month + Day + WeekDay + Snow + Holiday, data = rental_train_data);
#Serialize the model before saving it to the database table
trained_model <- as.raw(serialize(model_dtree, connection=NULL));
'
        , @input_data_1 = N'
            SELECT RentalCount
                 , Year
                 , Month
                 , Day
                 , WeekDay
                 , Snow
                 , Holiday
            FROM dbo.rental_data
            WHERE Year < 2015
            '
        , @input_data_1_name = N'rental_train_data'
        , @params = N'@trained_model varbinary(max) OUTPUT'
        , @trained_model = @trained_model OUTPUT;
END;
GO
```

## <a name="store-the-model-in-a-database-table"></a>Armazenar o modelo em uma tabela de banco de dados

Crie uma tabela no banco de dados TutorialDB e, em seguida, salve o modelo na tabela.

1. Crie uma tabela (`rental_models`) para armazenar o modelo.

    ```sql
    USE TutorialDB;
    DROP TABLE IF EXISTS rental_models;
    GO
    CREATE TABLE rental_models (
          model_name VARCHAR(30) NOT NULL DEFAULT('default model') PRIMARY KEY
        , model VARBINARY(MAX) NOT NULL
        );
    GO
    ```

1. Salve o modelo na tabela como um objeto binário, com o nome "DTree".

    ```sql
    -- Save model to table
    TRUNCATE TABLE rental_models;
    
    DECLARE @model VARBINARY(MAX);
    
    EXECUTE generate_rental_model @model OUTPUT;
    
    INSERT INTO rental_models (
          model_name
        , model
        )
    VALUES (
         'DTree'
        , @model
        );
    
    SELECT *
    FROM rental_models;
    ```

## <a name="create-a-stored-procedure-that-makes-predictions"></a>Criar um procedimento armazenado que faça previsões

Crie um procedimento armazenado (`predict_rentalcount_new`) que faz previsões usando o modelo treinado e um conjunto de dados novos.

```sql
-- Stored procedure that takes model name and new data as input parameters and predicts the rental count for the new data
USE [TutorialDB]
DROP PROCEDURE IF EXISTS predict_rentalcount_new;
GO
CREATE PROCEDURE predict_rentalcount_new (
      @model_name VARCHAR(100)
    , @input_query NVARCHAR(MAX)
    )
AS
BEGIN
    DECLARE @model VARBINARY(MAX) = (
            SELECT model
            FROM rental_models
            WHERE model_name = @model_name
            );

    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
#Convert types to factors
rentals$Month   <- factor(rentals$Month);
rentals$Day     <- factor(rentals$Day);
rentals$Holiday <- factor(rentals$Holiday);
rentals$Snow    <- factor(rentals$Snow);
rentals$WeekDay <- factor(rentals$WeekDay);

#Before using the model to predict, we need to unserialize it
rental_model <- unserialize(model);

#Call prediction function
rental_predictions <- predict(rental_model, rentals);
rental_predictions <- data.frame(rental_predictions);
'
        , @input_data_1 = @input_query
        , @input_data_1_name = N'rentals'
        , @output_data_1_name = N'rental_predictions'
        , @params = N'@model varbinary(max)'
        , @model = @model
    WITH RESULT SETS(("RentalCount_Predicted" FLOAT));
END;
GO
```

## <a name="execute-the-model-with-new-data"></a>Executar o modelo com novos dados

Agora, é possível usar o procedimento armazenado `predict_rentalcount_new` para prever o valor do aluguel com os novos dados.

```sql
-- Use the predict_rentalcount_new stored procedure with the model name and a set of features to predict the rental count
EXECUTE dbo.predict_rentalcount_new @model_name = 'DTree'
    , @input_query = '
        SELECT CONVERT(INT,  3) AS Month
             , CONVERT(INT, 24) AS Day
             , CONVERT(INT,  4) AS WeekDay
             , CONVERT(INT,  1) AS Snow
             , CONVERT(INT,  1) AS Holiday
        ';
GO
```

Você verá um resultado semelhante ao seguinte.

```results
RentalCount_Predicted
332.571428571429
```

Você criou, treinou e implantou com êxito um modelo em um banco de dados. Em seguida, você usou esse modelo em um procedimento armazenado para prever valores com base em novos dados.


## <a name="clean-up-resources"></a>Limpar os recursos

Quando terminar de usar o banco de dados TutorialDB, exclua-o do servidor.

## <a name="next-steps"></a>Próximas etapas

Na parte quatro desta série de tutoriais, você aprendeu a:

* Criar um procedimento armazenado que gera o modelo de machine learning
* Armazenar o modelo em uma tabela de banco de dados
* Criar um procedimento armazenado que faça previsões usando o modelo
* Executar o modelo com novos dados

Para saber mais sobre como usar o R nos Serviços de Machine Learning, confira:

* [Executar scripts simples do R](quickstart-r-create-script.md)
* [Estruturas, tipos e objetos de dados do R](quickstart-r-data-types-and-objects.md)
* [Funções do R](quickstart-r-functions.md)
