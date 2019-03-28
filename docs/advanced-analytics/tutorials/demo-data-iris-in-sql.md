---
title: Conjunto de dados íris demonstração de tutoriais do Python e R - aprendizagem de máquina do SQL Server
Description: Crie um banco de dados que contém o conjunto de dados íris e uma tabela para armazenar modelos. Esse conjunto de dados é usado em exercícios que mostra como encapsular a linguagem R ou o código do Python em um procedimento armazenado do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/19/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: f4a57f89a89ed8d5cbf81cc3d63fc1f19b42e51a
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510093"
---
#  <a name="iris-demo-data-for-python-and-r-tutorials-in-sql-server"></a>Dados de demonstração de íris para tutoriais do Python e R no SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Neste exercício, crie um banco de dados do SQL Server para armazenar dados do [conjunto de dados de flor de íris](https://en.wikipedia.org/wiki/Iris_flower_data_set) e modelos baseados nos mesmos dados. Dados íris estão incluídos nas distribuições do R e Python instaladas pelo SQL Server e são usados nos tutoriais de aprendizado de máquina para o SQL Server. 

Para concluir este exercício, você deve ter [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) ou outra ferramenta que pode executar consultas do T-SQL.

Tutoriais e guias de início rápido usando esse conjunto de dados incluem o seguinte:

+  [Guia de início rápido: Criar, treinar e usar um modelo de Python com procedimentos armazenados no SQL Server](quickstart-python-train-score-in-tsql.md)

## <a name="create-the-database"></a>Criar o banco de dados

1. Inicie o SQL Server Management Studio e abra um novo **consulta** janela.  

2. Criar um novo banco de dados para este projeto e alterar o contexto de sua **consulta** window para usar o novo banco de dados.

    ```sql
    CREATE DATABASE irissql
    GO
    USE irissql
    GO
    ```

    > [!TIP] 
    > Se você for novo no SQL Server, ou estiver trabalhando em um servidor que você possui, um erro comum é fazer logon e começar a trabalhar sem perceber que você está a **mestre** banco de dados. Para certificar-se de que você está usando o banco de dados correto, sempre especifique o contexto usando o `USE <database name>` instrução (por exemplo, `use irissql`).

3. Adicionar algumas tabelas vazias: um para armazenar os dados e outro para armazenar os modelos treinados. O **iris_models** tabela é usada para armazenar modelos serializados gerados em outros exercícios.

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
    > Se você for novo no T-SQL, vale a pena memorizar a `DROP...IF` instrução. Quando você tentar criar uma tabela e já existir, o SQL Server retornará um erro: "Já existe um objeto chamado 'iris_data' no banco de dados." Uma maneira de evitar esses erros é excluir todas as tabelas existentes ou outros objetos como parte do seu código.

4. Execute o seguinte código para criar a tabela usada para armazenar o modelo treinado. Para salvar modelos do Python (ou R) no SQL Server, eles devem ser serializados e armazenados em uma coluna do tipo **varbinary (max)**. 

    ```sql
    DROP TABLE IF EXISTS iris_models;
    GO
    
    CREATE TABLE iris_models (
      model_name VARCHAR(50) NOT NULL DEFAULT('default model') PRIMARY KEY,
      model VARBINARY(MAX) NOT NULL
    );
    GO
    ```

    Além do conteúdo de modelo, normalmente, você deve também adicionar colunas de outros metadados úteis, como o nome do modelo, a data em que ele foi treinado, o algoritmo de origem e os parâmetros, dados de origem e assim por diante. Agora vamos manter a simplicidade e use apenas o nome do modelo.

## <a name="populate-the-table"></a>Preencha a tabela

Você pode obter dados de íris internos de R ou Python. Você pode usar o Python ou R para carregar os dados em um quadro de dados e, em seguida, inseri-lo em uma tabela no banco de dados. Movendo dados de treinamento de uma sessão externa para uma tabela do SQL Server é um processo de várias etapas:

+ Crie um procedimento armazenado que obtém os dados desejados.
+ Execute o procedimento armazenado para realmente obter os dados.
+ Construa uma instrução INSERT para especificar onde os dados recuperados devem ser salvo.

1. Em sistemas com a integração do Python, crie o seguinte procedimento armazenado que usa o código do Python para carregar os dados.

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

    Quando você executa esse código, você deve receber a mensagem "Comandos concluídos com êxito." Todos os isso significa é que o procedimento armazenado foi criado de acordo com suas especificações.

2. Como alternativa, em sistemas com a integração do R, crie um procedimento que usa o R em vez disso.

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

3. Na verdade, popular a tabela, execute o procedimento armazenado e especificar a tabela em que os dados devem ser gravados. Quando executado, o procedimento armazenado executa o código Python ou R, que carrega o conjunto de dados íris interno e, em seguida, insere os dados na **iris_data** tabela.

    ```sql
    INSERT INTO iris_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species", "SpeciesId")
    EXEC dbo.get_iris_dataset;
    ```

    Se você for novo no T-SQL, lembre-se de que a instrução INSERT apenas adiciona novos dados; ele não verificar dados existentes, ou exclua e recrie a tabela. Para evitar obter várias cópias dos mesmos dados em uma tabela, você pode executar essa instrução primeiro: `TRUNCATE TABLE iris_data`. O T-SQL [TRUNCATE TABLE](https://docs.microsoft.com/sql/t-sql/statements/truncate-table-transact-sql) instrução exclui dados existentes, mas mantém a estrutura da tabela intacto.

    > [!TIP]
    > Para modificar o procedimento armazenado mais tarde, você não precisa descarte e recrie-o. Use o [ALTER PROCEDURE](https://docs.microsoft.com/sql/t-sql/statements/alter-procedure-transact-sql) instrução. 


## <a name="query-the-data"></a>Consultar os dados

Como uma etapa de validação, execute uma consulta para confirmar se que os dados foram carregados.

1. No Pesquisador de objetos em bancos de dados, clique com botão direito do **irissql** de banco de dados e iniciar uma nova consulta.

2. Execute algumas consultas simples:

    ```sql
    SELECT TOP(10) * FROM iris_data;
    SELECT COUNT(*) FROM iris_data;
    ```

## <a name="next-steps"></a>Próximas etapas

O seguinte guia de início rápido, você criará um modelo de aprendizado de máquina e salvá-lo em uma tabela e, em seguida, usar o modelo para gerar os resultados previstos.

+ [Guia de início rápido: Criar, treinar e usar um modelo de Python com procedimentos armazenados no SQL Server](quickstart-python-train-score-in-tsql.md)
