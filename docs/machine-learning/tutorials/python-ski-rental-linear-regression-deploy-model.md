---
title: 'Tutorial do Python: Implantar modelo'
titleSuffix: SQL machine learning
description: Na parte quatro desta série de tutoriais de quatro partes, você implantará um modelo de Python para prever os aluguéis de esqui em um banco de dados com o aprendizado de máquina do SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/21/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 030a172d35800becce17f804f67973368581fc05
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730489"
---
# <a name="python-tutorial-deploy-a-linear-regression-model-with-sql-machine-learning"></a>Tutorial do Python: implantar um modelo de regressão linear com o aprendizado de máquina do SQL
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Na parte quatro desta série de tutoriais de quatro partes, você implantará um modelo de regressão linear desenvolvido em Python em um banco de dados do SQL Server que usa os Serviços de Machine Learning ou os Clusters de Big Data.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Na parte quatro desta série de tutoriais de quatro partes, você implantará um modelo de regressão linear desenvolvido em Python em um banco de dados do SQL Server que usa os Serviços de Machine Learning.
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
Na parte quatro desta série de tutoriais de quatro partes, você implantará um modelo de regressão linear desenvolvido em Python em um banco de dados de Instância Gerenciada de SQL do Azure que usa os Serviços de Machine Learning.
::: moniker-end

Neste artigo, você aprenderá a:

> [!div class="checklist"]
> * Criar um procedimento armazenado que gera o modelo de machine learning
> * Armazenar o modelo em uma tabela de banco de dados
> * Criar um procedimento armazenado que faça previsões usando o modelo
> * Executar o modelo com novos dados

Na [parte um](python-ski-rental-linear-regression.md), você aprendeu a restaurar o banco de dados de exemplo.

Na [parte dois](python-ski-rental-linear-regression-prepare-data.md), você aprendeu a carregar os dados de um banco de dados em uma estrutura de dados do Python e a prepará-los no Python.

Na [parte três](python-ski-rental-linear-regression-train-model.md), você aprendeu como treinar um modelo de machine learning de regressão linear no Python.

## <a name="prerequisites"></a>Pré-requisitos

* A parte quatro deste tutorial pressupõe que você concluiu a [parte um](python-ski-rental-linear-regression.md) e os respectivos pré-requisitos.

## <a name="create-a-stored-procedure-that-generates-the-model"></a>Criar o procedimento armazenado que gera o modelo

Agora, usando os scripts Python que você desenvolveu, crie um procedimento armazenado **generate_rental_py_model** que treina e gera o modelo de regressão linear usando LinearRegression da Scikit-learn.

Execute a instrução do T-SQL a seguir no Azure Data Studio para criar o procedimento armazenado para treinar o modelo.

```sql
-- Stored procedure that trains and generates a Python model using the rental_data and a decision tree algorithm
DROP PROCEDURE IF EXISTS generate_rental_py_model;
go
CREATE PROCEDURE generate_rental_py_model (@trained_model varbinary(max) OUTPUT)
AS
BEGIN
    EXECUTE sp_execute_external_script
      @language = N'Python'
    , @script = N'
from sklearn.linear_model import LinearRegression
import pickle

df = rental_train_data

# Get all the columns from the dataframe.
columns = df.columns.tolist()

# Store the variable well be predicting on.
target = "RentalCount"

# Initialize the model class.
lin_model = LinearRegression()

# Fit the model to the training data.
lin_model.fit(df[columns], df[target])

# Before saving the model to the DB table, convert it to a binary object
trained_model = pickle.dumps(lin_model)'

, @input_data_1 = N'select "RentalCount", "Year", "Month", "Day", "WeekDay", "Snow", "Holiday" from dbo.rental_data where Year < 2015'
, @input_data_1_name = N'rental_train_data'
, @params = N'@trained_model varbinary(max) OUTPUT'
, @trained_model = @trained_model OUTPUT;
END;
GO
```

## <a name="store-the-model-in-a-database-table"></a>Armazenar o modelo em uma tabela de banco de dados

Crie uma tabela no banco de dados TutorialDB e, em seguida, salve o modelo na tabela.

1. Execute a seguinte instrução T-SQL no Azure Data Studio para criar uma tabela chamada **dbo.rental_py_models**, que é usada para armazenar o modelo.

   ```sql
   USE TutorialDB;
   DROP TABLE IF EXISTS dbo.rental_py_models;
   GO
   CREATE TABLE dbo.rental_py_models (
       model_name VARCHAR(30) NOT NULL DEFAULT('default model') PRIMARY KEY,
       model VARBINARY(MAX) NOT NULL
   );
   GO
   ```

1. Salve o modelo na tabela como um objeto binário, com o nome de modelo **linear_model**.

   ```sql
   DECLARE @model VARBINARY(MAX);
   EXECUTE generate_rental_py_model @model OUTPUT;
   
   INSERT INTO rental_py_models (model_name, model) VALUES('linear_model', @model);
   ```

## <a name="create-a-stored-procedure-that-makes-predictions"></a>Criar um procedimento armazenado que faça previsões

1. Crie um procedimento armazenado **py_predict_rentalcount** que faça previsões usando o modelo treinado e um conjunto de novos dados. Execute o T-SQL abaixo no Azure Data Studio.

   ```sql
   DROP PROCEDURE IF EXISTS py_predict_rentalcount;
   GO
   CREATE PROCEDURE py_predict_rentalcount (@model varchar(100))
   AS
   BEGIN
       DECLARE @py_model varbinary(max) = (select model from rental_py_models where model_name = @model);
   
       EXECUTE sp_execute_external_script
                   @language = N'Python',
                   @script = N'
   
   # Import the scikit-learn function to compute error.
   from sklearn.metrics import mean_squared_error
   import pickle
   import pandas
   
   rental_model = pickle.loads(py_model)
   
   df = rental_score_data
   
   # Get all the columns from the dataframe.
   columns = df.columns.tolist()
   
   # Variable you will be predicting on.
   target = "RentalCount"
   
   # Generate the predictions for the test set.
   lin_predictions = rental_model.predict(df[columns])
   print(lin_predictions)
   
   # Compute error between the test predictions and the actual values.
   lin_mse = mean_squared_error(lin_predictions, df[target])
   #print(lin_mse)
   
   predictions_df = pandas.DataFrame(lin_predictions)
   
   OutputDataSet = pandas.concat([predictions_df, df["RentalCount"], df["Month"], df["Day"], df["WeekDay"], df["Snow"], df["Holiday"], df["Year"]], axis=1)
   '
   , @input_data_1 = N'Select "RentalCount", "Year" ,"Month", "Day", "WeekDay", "Snow", "Holiday"  from rental_data where Year = 2015'
   , @input_data_1_name = N'rental_score_data'
   , @params = N'@py_model varbinary(max)'
   , @py_model = @py_model
   with result sets (("RentalCount_Predicted" float, "RentalCount" float, "Month" float,"Day" float,"WeekDay" float,"Snow" float,"Holiday" float, "Year" float));
   
   END;
   GO
    ```

1. Criar uma tabela para armazenar as previsões.

   ```sql
   DROP TABLE IF EXISTS [dbo].[py_rental_predictions];
   GO
   
   CREATE TABLE [dbo].[py_rental_predictions](
    [RentalCount_Predicted] [int] NULL,
    [RentalCount_Actual] [int] NULL,
    [Month] [int] NULL,
    [Day] [int] NULL,
    [WeekDay] [int] NULL,
    [Snow] [int] NULL,
    [Holiday] [int] NULL,
    [Year] [int] NULL
   ) ON [PRIMARY]
   GO
   ```

1. Executar o procedimento armazenado para prever contagens de aluguel

   ```sql
   --Insert the results of the predictions for test set into a table
   INSERT INTO py_rental_predictions
   EXEC py_predict_rentalcount 'linear_model';
   
   -- Select contents of the table
   SELECT * FROM py_rental_predictions;
   ```

   Você deverá ver resultados semelhantes aos seguintes.

   :::image type="content" source="media/python-tutorial-prediction-results.png" alt-text="Resultados da previsão do procedimento armazenado":::

Você criou, treinou e implantou um modelo com êxito. Em seguida, você usou esse modelo em um procedimento armazenado para prever valores com base em novos dados.

## <a name="next-steps"></a>Próximas etapas

Na parte quatro desta série de tutoriais, você concluiu estas etapas:

* Criar um procedimento armazenado que gera o modelo de machine learning
* Armazenar o modelo em uma tabela de banco de dados
* Criar um procedimento armazenado que faça previsões usando o modelo
* Executar o modelo com novos dados

Para saber mais sobre como usar o Python no aprendizado de máquina do SQL, confira:

+ [Tutoriais do Python](python-tutorials.md)
