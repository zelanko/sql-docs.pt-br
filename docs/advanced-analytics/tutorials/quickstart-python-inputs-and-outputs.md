---
title: Guia de início rápido para trabalhar com entradas e saídas em Python – Machine Learning do SQL Server
description: Neste início rápido para o script Python no SQL Server, saiba como estruturar as entradas e saídas para o procedimento armazenado do sistema de sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: a778c4a65b9e3f4cbf4ed77cff46e9061d4b6a8a
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59583219"
---
# <a name="quickstart-handle-inputs-and-outputs-using-python-in-sql-server"></a>Início Rápido: Lidar com entradas e saídas usando o Python no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Neste início rápido mostra como lidar com entradas e saídas ao usar o Python em serviços do SQL Server Machine Learning.

Por padrão, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) aceita um único conjunto de dados entrado, que normalmente você fornece na forma de uma consulta SQL válida.

Outros tipos de entrada podem ser passados como variáveis SQL: por exemplo, você pode passar um modelo treinado como uma variável, usando uma função de serialização, como [pickle](https://docs.python.org/3.0/library/pickle.html) ou [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) para gravar o modelo um formato binário.

O procedimento armazenado retorna um único Python [pandas](https://pandas.pydata.org/pandas-docs/stable/index.html) de estruturas de dados como saída, mas você também pode gerar modelos como variáveis e escalares. Por exemplo, você pode gerar um modelo treinado como uma variável binária e passá-lo para uma instrução T-SQL INSERT, para gravar esse modelo em uma tabela. Você também pode gerar plotagens (em formato binário) ou escalares (valores individuais, como a data e hora, o tempo decorrido para treinar o modelo e assim por diante).

## <a name="prerequisites"></a>Prerequisites

Um início rápido anterior, [Python Verifique se existe no SQL Server](quickstart-python-verify.md), fornece informações e links para configurar o ambiente do Python necessário para este início rápido.

## <a name="create-the-source-data"></a>Criar os dados de origem

Crie uma pequena tabela de dados de teste executando a seguinte instrução T-SQL:

```sql
CREATE TABLE PythonTestData (col1 INT NOT NULL)
INSERT INTO PythonTestData VALUES (1);
INSERT INTO PythonTestData VALUES (10);
INSERT INTO PythonTestData VALUES (100);
GO
```

Assim que a tabela tiver sido criada, use a seguinte instrução para consultar a tabela:
  
```sql
SELECT * FROM PythonTestData
```

**Resultados**

![Conteúdo da tabela PythonTestData](./media/select-pythontestdata.png)

## <a name="inputs-and-outputs"></a>Entradas e Saídas

Vamos dar uma olhada no padrão variáveis de entrada e saídas de sp_execute_external_script: `InputDataSet` e `OutputDataSet`.

1. Você pode obter os dados da tabela como entrada para seu script R. Execute a instrução a seguir. Obtém os dados da tabela, faz uma viagem de ida e por meio de execução R e retornar os valores com o nome da coluna *NewColName*.

    Os dados retornados pela consulta são passados para o tempo de execução de R, que retorna os dados ao banco de dados SQL como um quadro de dados. A cláusula WITH RESULT SETS define o esquema da tabela de dados retornados para o banco de dados SQL.

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'Python'
        , @script = N'OutputDataSet = InputDataSet;'
        , @input_data_1 = N'SELECT * FROM PythonTestData;'
    WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    **Resultados**

    ![Saída do script de Python que retorna dados de uma tabela](./media/python-output-pythontestdata.png)

2. Vamos alterar o nome das variáveis de entrada ou saídas. O script acima usado o padrão de entrada e saída de nomes de variáveis _InputDataSet_ e _OutputDataSet_. Para definir os dados de entrada associados _InputDatSet_, você usa o *@input_data_1* variável.

    Nesse script, os nomes das variáveis de entrada e saída para o procedimento armazenado foi alterados para *SQL_out* e *SQL_in*:

    ```sql
    EXECUTE sp_execute_external_script
      @language = N'Python'
      , @script = N'SQL_out = SQL_in'
      , @input_data_1 = N' SELECT 12 as Col;'
      , @input_data_1_name  = N'SQL_in'
      , @output_data_1_name =  N'SQL_out'
      WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    No caso das variáveis de entrada e saídas no `@input_data_1_name` e `@output_data_1_name` precisa corresponder ao caso das, em que o código do Python no `@script`, como Python diferencia maiusculas de minúsculas.

    Apenas um conjunto de dados de entrada pode ser passado como um parâmetro e é possível retornar apenas um conjunto de dados. No entanto, você pode chamar outros conjuntos de dados dentro de seu código Python e é possível retornar saídas de outros tipos, além do conjunto de dados. Você também pode adicionar a palavra-chave OUTPUT a qualquer parâmetro para que ele seja retornado com os resultados. 

    O `WITH RESULT SETS` instrução define o esquema para os dados que são usados no SQL Server. Você precisará fornecer tipos de dados compatíveis do SQL para cada coluna retornada do Python. Você pode usar a definição de esquema para fornecer novos nomes de coluna muito, pois você não precisará usar os nomes de coluna do Frame Python.

3. Você também pode gerar valores usando o script de Python e deixar a cadeia de caracteres de consulta de entrada em _@input_data_1_ em branco.

    ```sql
    EXECUTE sp_execute_external_script
    @language = N'Python'
    , @script = N'
    import pandas as pd
    mytextvariable = pandas.Series(["hello", " ", "world"]);
    OutputDataSet = pd.DataFrame(mytextvariable);'
    , @input_data_1 = N''
    WITH RESULT SETS (([Col1] CHAR(20) NOT NULL));
    ```

    **Resultados**

    ![Os resultados da consulta usando @script como entrada](./media/python-data-generated-output.png)

## <a name="next-steps"></a>Próximas etapas

Examine alguns dos problemas que podem ocorrer ao passar dados tabulares entre Python e o SQL Server.

> [!div class="nextstepaction"]
> [Guia de início rápido: Estruturas de dados do Python no SQL Server](quickstart-python-data-structures.md)