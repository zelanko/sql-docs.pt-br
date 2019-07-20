---
title: Conjunto de dados de demonstração da íris para tutoriais do Python e do R
Description: Crie um banco de dados que contenha o DataSet íris e uma tabela para armazenar modelos. Esse conjunto de DataSet é usado em exercícios que mostram como encapsular a linguagem R ou o código Python em um procedimento armazenado SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/19/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 5050fc0d0fcbb6c70b7aabea1b67d75cc686b96b
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345226"
---
#  <a name="iris-demo-data-for-python-and-r-tutorials-in-sql-server"></a>Dados de demonstração da íris para tutoriais de Python e R no SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Neste exercício, crie um banco de dados SQL Server para armazenar dados de modelos e de [flores de íris](https://en.wikipedia.org/wiki/Iris_flower_data_set) com base nos mesmos dados. Os dados de íris são incluídos nas distribuições do R e do Python instaladas pelo SQL Server e são usados nos tutoriais do Machine Learning para SQL Server. 

Para concluir este exercício, você deve ter [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) ou outra ferramenta que possa executar consultas T-SQL.

Os tutoriais e os guias de início rápido usando esse conjunto de dados incluem o seguinte:

+  [Início Rápido: Criar, treinar e usar um modelo Python com procedimentos armazenados no SQL Server](quickstart-python-train-score-in-tsql.md)

## <a name="create-the-database"></a>Criar o banco de dados

1. Inicie SQL Server Management Studio e abra uma nova janela de **consulta** .  

2. Crie um novo banco de dados para este projeto e altere o contexto da janela de **consulta** para usar o novo banco de dados.

    ```sql
    CREATE DATABASE irissql
    GO
    USE irissql
    GO
    ```

    > [!TIP] 
    > Se você for novo no SQL Server ou estiver trabalhando em um servidor que possui, um erro comum é fazer logon e começar a trabalhar sem perceber que você está no banco de dados **mestre** . Para ter certeza de que você está usando o banco de dados correto, sempre especifique o `USE <database name>` contexto usando a instrução ( `use irissql`por exemplo,).

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

    > [!TIP] 
    > Se você for novo no T-SQL, ele pagará memorizar a `DROP...IF` instrução. Quando você tenta criar uma tabela e uma já existe, SQL Server retorna um erro: "Já existe um objeto chamado ' iris_data ' no banco de dados." Uma maneira de evitar esses erros é excluir todas as tabelas existentes ou outros objetos como parte do seu código.

4. Execute o código a seguir para criar a tabela usada para armazenar o modelo treinado. Para salvar modelos de Python (ou R) em SQL Server, eles devem ser serializados e armazenados em uma coluna do tipo **varbinary (max)** . 

    ```sql
    DROP TABLE IF EXISTS iris_models;
    GO
    
    CREATE TABLE iris_models (
      model_name VARCHAR(50) NOT NULL DEFAULT('default model') PRIMARY KEY,
      model VARBINARY(MAX) NOT NULL
    );
    GO
    ```

    Além do conteúdo do modelo, normalmente, você também adicionaria colunas para outros metadados úteis, como o nome do modelo, a data em que foi treinado, o algoritmo de origem e os parâmetros, os dados de origem e assim por diante. Por enquanto, vamos manter isso simples e usar apenas o nome do modelo.

## <a name="populate-the-table"></a>Popular a tabela

Você pode obter dados de íris internos do R ou do Python. Você pode usar o Python ou o R para carregar os dados em um quadro de dados e, em seguida, inseri-los em uma tabela no banco de dado. Mover dados de treinamento de uma sessão externa para uma tabela SQL Server é um processo de várias etapas:

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

    Ao executar esse código, você deve receber a mensagem "comandos concluídos com êxito". Tudo isso significa que o procedimento armazenado foi criado de acordo com suas especificações.

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

3. Para realmente preencher a tabela, execute o procedimento armazenado e especifique a tabela em que os dados devem ser gravados. Quando executado, o procedimento armazenado executa o código Python ou R, que carrega o conjunto de dados íris interno e, em seguida, insere os dados na tabela **iris_data** .

    ```sql
    INSERT INTO iris_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species", "SpeciesId")
    EXEC dbo.get_iris_dataset;
    ```

    Se você for novo no T-SQL, lembre-se de que a instrução INSERT só adiciona novos dados; Ele não verificará os dados existentes ou excluirá e recriará a tabela. Para evitar a obtenção de várias cópias dos mesmos dados em uma tabela, você pode executar esta instrução primeiro `TRUNCATE TABLE iris_data`:. A instrução T-SQL [TRUNCATE TABLE](https://docs.microsoft.com/sql/t-sql/statements/truncate-table-transact-sql) exclui dados existentes, mas mantém a estrutura da tabela intacta.

    > [!TIP]
    > Para modificar o procedimento armazenado posteriormente, você não precisa descartá-lo e recriá-lo. Use a instrução [ALTER PROCEDURE](https://docs.microsoft.com/sql/t-sql/statements/alter-procedure-transact-sql) . 


## <a name="query-the-data"></a>Consultar os dados

Como uma etapa de validação, execute uma consulta para confirmar se os dados foram carregados.

1. No Pesquisador de objetos, em bancos de dados, clique com o botão direito do mouse em **irissql** e inicie uma nova consulta.

2. Execute algumas consultas simples:

    ```sql
    SELECT TOP(10) * FROM iris_data;
    SELECT COUNT(*) FROM iris_data;
    ```

## <a name="next-steps"></a>Próximas etapas

No guia de início rápido a seguir, você criará um modelo de aprendizado de máquina e o salvará em uma tabela e, em seguida, usará o modelo para gerar resultados previstos.

+ [Início Rápido: Criar, treinar e usar um modelo Python com procedimentos armazenados no SQL Server](quickstart-python-train-score-in-tsql.md)
