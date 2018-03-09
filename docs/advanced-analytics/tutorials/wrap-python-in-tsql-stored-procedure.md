---
title: "Encapsular o código Python em um procedimento armazenado | Microsoft Docs"
titleSuffix: SQL Server
ms.custom: 
ms.date: 02/28/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2017
dev_langs:
- Python
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 11b5b649a942b1d1804b799426530a1b82ee9458
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
# <a name="wrap-python-code-in-a-stored-procedure"></a>Encapsular o código Python em um procedimento armazenado
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Em um [lição anterior](run-python-using-t-sql.md), você aprendeu como tornar Python falar com o SQL Server. Nesta lição, você aprenderá como incorporar o código Python em um procedimento armazenado, para obter dados dos conjuntos de dados de amostra do Python e gravar dados em uma tabela do SQL Server.

Procedimento armazenado do sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) fornece o wrapper que passa variáveis SQL e conjuntos de dados do SQL em Python. Também trata dos resultados produzidos pelo Python e transmite-as para SQL Server em um formato compatível com tipos de dados SQL.

Vamos ver como isso funciona.

## <a name="prepare-the-database-and-tables"></a>Preparar o banco de dados e tabelas

Embora seja possível configurar um cliente remoto e executar o código Python usando o código do Visual Studio, o Visual Studio, PyCharm ou outras ferramentas para simplificar o cenário, todo o código nesta lição deve ser executado como parte de um procedimento armazenado.

1. Inicie o SQL Server Management Studio e abra um novo **consulta** janela.  

2. Criar um novo banco de dados para este projeto e alterar o contexto de sua **consulta** janela para usar o novo banco de dados.

    ```sql
    CREATE DATABASE sqlpy;
    GO;
    USE sqlpy;
    GO;
    ```

    > [!TIP] 
    > Se você é novo no SQL Server ou se estiver trabalhando em um servidor que você possui, um erro comum é fazer logon e começar a trabalhar sem perceba que você está a **mestre** banco de dados. Para certificar-se de que você está usando o banco de dados correto, sempre especifique o contexto usando o `USE <database name>` instrução.

3. Adicionar algumas tabelas vazias: uma para armazenar os dados e outra para armazenar os modelos de treinar. Mais tarde você pode preencher as tabelas usando Python.

    O código a seguir cria a tabela de dados de treinamento.

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

    Se você for novo no T-SQL, vale a pena memorizar a `DROP...IF` instrução. Quando você tenta criar uma tabela e já existir, o SQL Server retorna um erro: "Já existe um objeto chamado 'iris_data' no banco de dados." Uma maneira para evitar esses erros é excluir todas as tabelas existentes ou outros objetos como parte do seu código.

4. Execute o seguinte código para criar a tabela usada para armazenar o modelo treinado. Para salvar modelos Python (ou R) no SQL Server, eles devem ser serializados e armazenados em uma coluna do tipo **varbinary (max)**. 

    ```sql
    DROP TABLE IF EXISTS iris_models;
    GO
    
    CREATE TABLE iris_models (
      model_name VARCHAR(50) NOT NULL DEFAULT('default model') PRIMARY KEY,
      model VARBINARY(MAX) NOT NULL
    );
    GO
    ```

    Além do conteúdo do modelo, normalmente, você deve também adicionar colunas para outros metadados úteis, como o nome do modelo, a data que foi treinado, o algoritmo de origem e os parâmetros, dados de origem e assim por diante. Agora vamos manter a simplicidade e use apenas o nome do modelo.

## <a name="populate-the-table"></a>Preencha a tabela

Para mover os dados de treinamento do Python para um SQL Server a tabela é um processo de várias etapas:

+ Criar um procedimento armazenado que obtém os dados desejados.
+ Executar o procedimento armazenado para realmente obter os dados.
+ Você pode usar uma instrução INSERT para especificar onde os dados recuperados devem ser salvo.

1. Crie o seguinte procedimento armazenado que inclui o código Python. 

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

    Quando você executa esse código, você deve receber a mensagem "Comandos concluída com êxito." Todos os isso significa é que o procedimento armazenado foi criado de acordo com suas especificações.

2. Preencha a tabela, execute o procedimento armazenado e especificar a tabela onde os dados devem ser gravados. Quando executado, o procedimento armazenado executa o código Python, que carrega o conjunto de dados Iris dos dados de exemplo do Python internos.

    ```sql
    INSERT INTO iris_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species", "SpeciesId")
    EXEC dbo.get_iris_dataset;
    ```

    Se você estiver familiarizado com o T-SQL, lembre-se de que a instrução INSERT apenas adiciona novos dados; ele não verificar dados existentes, ou exclua e recrie a tabela. Para evitar várias cópias dos mesmos dados em uma tabela, você pode executar essa instrução primeiro: `TRUNCATE TABLE iris_data`. O T-SQL [TRUNCATE TABLE](https://docs.microsoft.com/sql/t-sql/statements/truncate-table-transact-sql) instrução exclui os dados existentes, mas mantém a estrutura da tabela intacto.

    > [!TIP]
    > Para modificar o procedimento armazenado mais tarde, você não precisa descarte e recrie-o. Use o [ALTER PROCEDURE](https://docs.microsoft.com/sql/t-sql/statements/alter-procedure-transact-sql) instrução. 

3. Para verificar se os dados foram carregados corretamente, você pode executar algumas consultas simples:

    ```sql
    SELECT TOP(10) * FROM iris_data;
    SELECT COUNT(*) FROM iris_data;
    ```

No [próxima lição](../tutorials/train-score-using-python-in-tsql.md), criar um modelo de aprendizado de máquina e salvá-lo em uma tabela.

### <a name="further-reading-about-stored-procedures"></a>Ler mais sobre procedimentos armazenados

Se você for novo no SQL Server, pode ser complicados à primeira de procedimentos armazenados. Mas um procedimento armazenado é uma interface poderosa e flexível para passar dados entre aplicativos e o servidor. Usando um procedimento armazenado, você pode dinamicamente definir entradas, que torna mais fácil passar em novos nomes de modelo, novos parâmetros e novos dados, sem alterar o código Python.

Para obter uma visão geral do trabalho de procedimentos armazenados como, consulte [procedimentos armazenados (mecanismo de banco de dados)](https://docs.microsoft.com/sql/relational-databases/stored-procedures/stored-procedures-database-engine), ou este tutorial: [escrever instruções de Transact-SQL](https://docs.microsoft.com/sql/t-sql/tutorial-writing-transact-sql-statements).

Há também alguns bons tutoriais em sites de comunidade, como [SQL Server Central](http://www.sqlservercentral.com/) ou [equipe SQL](http://www.sqlteam.com/).

Como você pensar em como você pode encapsular melhor o código Python no T-SQL, considere também usar esses recursos:

+ Definindo valores padrão para o procedimento armazenado
+ Usando a palavra-chave OUTPUT ao passar variáveis de entrada
+ Criando definições de esquema usando com resultados para garantir que os dados consumidos por aplicativos tem os nomes de coluna e tipos de dados
+ Fornecendo dicas para melhorar o processamento em lotes
+ Representando um usuário diferente para testar seu código, usando EXECUTE AS cláusula

## <a name="next-lesson"></a>Próxima lição

[Treinar um modelo de Python e gerar pontuações no SQL Server](../tutorials/train-score-using-python-in-tsql.md)