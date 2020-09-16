---
description: Dados de demonstração do Iris para tutoriais de Python e R com machine learning do SQL
title: Conjunto de dados de demonstração do Iris para tutoriais
titleSuffix: SQL machine learning
Description: Crie um banco de dados que contenha o conjunto de dados do Iris e modelos de previsão. Esse conjunto de dados é usado em tutoriais de R e Python com machine learning do SQL.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 05/26/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: e5a1f9c36b6dc59988951a693be05b4e10e580f4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494999"
---
# <a name="iris-demo-data-for-python-and-r-tutorials-with-sql-machine-learning"></a>Dados de demonstração do Iris para tutoriais de Python e R com machine learning do SQL
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

Neste exercício, crie um banco de dados para armazenar dados do [conjunto de dados de flores do Iris](https://en.wikipedia.org/wiki/Iris_flower_data_set) e modelos baseados nos mesmos dados. Os dados do Iris são incluídos nas distribuições do R e do Python e são usados nos tutoriais de machine learning do SQL Server.

Para concluir este exercício, você deve ter o [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) ou outra ferramenta que possa executar consultas T-SQL.

Os tutoriais e guias de início rápido que usam esse conjunto de dados incluem o seguinte:

+ [Início Rápido: Criar e pontuar um modelo preditivo no Python](quickstart-python-train-score-model.md)

## <a name="create-the-database"></a>Criar o banco de dados

1. Inicie o SQL Server Management Studio e abra uma nova janela de **Consulta**.  

2. Crie um novo banco de dados para este projeto e altere o contexto de sua janela **Consulta** para usar o novo banco de dados.

    ```sql
    CREATE DATABASE irissql
    GO
    USE irissql
    GO
    ```

3. Adicione algumas tabelas vazias: uma para armazenar os dados e outra para armazenar os modelos treinados. A tabela **iris_models** é usada para armazenar modelos serializados gerados em outros exercícios.

    O código a seguir cria a tabela para os dados de treinamento.

    ```sql
    DROP TABLE IF EXISTS iris_data;
    GO
    CREATE TABLE iris_data (
      id INT NOT NULL IDENTITY PRIMARY KEY
      , "Sepal.Length" FLOAT NOT NULL, "Sepal.Width" FLOAT NOT NULL
      , "Petal.Length" FLOAT NOT NULL, "Petal.Width" FLOAT NOT NULL
      , "Species" VARCHAR(100) NOT NULL, "SpeciesId" INT NOT NULL
    );
    ```

4. Execute o código a seguir para criar a tabela usada para armazenar o modelo treinado. Para salvar modelos de Python (ou R) no SQL Server, eles devem ser serializados e armazenados em uma coluna do tipo **varbinary(max)** .

    ```sql
    DROP TABLE IF EXISTS iris_models;
    GO

    CREATE TABLE iris_models (
      model_name VARCHAR(50) NOT NULL DEFAULT('default model') PRIMARY KEY,
      model VARBINARY(MAX) NOT NULL
    );
    GO
    ```

    Além do conteúdo do modelo, normalmente, você também adicionaria colunas a outros metadados úteis, como o nome do modelo, a data em que foi treinado, o algoritmo de origem e os parâmetros, os dados de origem e assim por diante. Por enquanto, vamos manter isso simples e usar apenas o nome do modelo.

## <a name="populate-the-table"></a>Popular a tabela

É possível obter dados internos do Iris do R ou do Python. Você pode usar o Python ou o R para carregar os dados em um quadro de dados e, em seguida, inseri-los em uma tabela no banco de dados. Mover dados de treinamento de uma sessão externa para uma tabela é um processo de várias etapas:

+ Crie um procedimento armazenado que obtenha os dados desejados.
+ Execute o procedimento armazenado para realmente obter os dados.
+ Construa uma instrução INSERT para especificar onde os dados recuperados devem ser salvos.

1. Em sistemas com integração do Python, crie o procedimento armazenado a seguir que usa o código Python para carregar os dados.

    ```sql
    CREATE PROCEDURE get_iris_dataset
    AS
    BEGIN
    EXEC sp_execute_external_script @language = N'Python', 
    @script = N'
    from sklearn import datasets
    iris = datasets.load_iris()
    iris_data = pandas.DataFrame(iris.data)
    iris_data["Species"] = pandas.Categorical.from_codes(iris.target, iris.target_names)
    iris_data["SpeciesId"] = iris.target
    ', 
    @input_data_1 = N'', 
    @output_data_1_name = N'iris_data'
    WITH RESULT SETS (("Sepal.Length" float not null, "Sepal.Width" float not null, "Petal.Length" float not null, "Petal.Width" float not null, "Species" varchar(100) not null, "SpeciesId" int not null));
    END;
    GO
    ```

    Ao executar esse código, você deve receber a mensagem "Comandos concluídos com êxito". Tudo isso significa que o procedimento armazenado foi criado de acordo com suas especificações.

2. Como alternativa, em sistemas com a integração do R, crie um procedimento que usa R em vez disso.

    ```sql
    CREATE PROCEDURE get_iris_dataset
    AS
    BEGIN
    EXEC sp_execute_external_script @language = N'R', 
    @script = N'
    library(RevoScaleR)
    data(iris)
    iris$SpeciesID <- c(unclass(iris$Species))
    iris_data <- iris
    ', 
    @input_data_1 = N'', 
    @output_data_1_name = N'iris_data'
    WITH RESULT SETS (("Sepal.Length" float not null, "Sepal.Width" float not null, "Petal.Length" float not null, "Petal.Width" float not null, "Species" varchar(100) not null, "SpeciesId" int not null));
    END;
    GO
    ```

3. Para realmente popular a tabela, execute o procedimento armazenado e especifique a tabela em que os dados devem ser escritos. Quando executado, o procedimento armazenado executa o código Python ou R, que carrega o conjunto de dados interno do Iris e, em seguida, insere os dados na tabela **iris_data**.

    ```sql
    INSERT INTO iris_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species", "SpeciesId")
    EXEC dbo.get_iris_dataset;
    ```

    Se você for novato no T-SQL, lembre-se de que a instrução INSERT só adiciona novos dados; ela não verificará os dados existentes ou excluirá e recompilará a tabela. Para evitar a obtenção de várias cópias dos mesmos dados em uma tabela, você pode executar esta instrução primeiro: `TRUNCATE TABLE iris_data`. A instrução T-SQL [TRUNCATE TABLE](https://docs.microsoft.com/sql/t-sql/statements/truncate-table-transact-sql) exclui os dados existentes, mas mantém a estrutura da tabela intacta.

## <a name="query-the-data"></a>Consultar os dados

Como uma etapa de validação, execute uma consulta para confirmar se os dados foram carregados.

1. No Pesquisador de Objetos, em "Bancos de dados", clique com o botão direito do mouse no banco de dados **irissql** e inicie uma nova consulta.

2. Execute algumas consultas simples:

    ```sql
    SELECT TOP(10) * FROM iris_data;
    SELECT COUNT(*) FROM iris_data;
    ```

## <a name="next-steps"></a>Próximas etapas

No início rápido a seguir, você criará um modelo de machine learning e o salvará em uma tabela. Em seguida, usará o modelo para gerar resultados previstos.

+ [Início rápido: criar e pontuar um modelo preditivo no Python](quickstart-python-train-score-model.md)
