---
title: Início rápido para trabalhar com entradas e saídas no Python
description: Neste guia de início rápido para o script Python no SQL Server, saiba como estruturar entradas e saídas para o procedimento armazenado do sistema sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 10c62f78ff2ac23e33ad251a07ed8f3689f79843
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715461"
---
# <a name="quickstart-handle-inputs-and-outputs-using-python-in-sql-server"></a>Início Rápido: Manipular entradas e saídas usando o Python no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este guia de início rápido mostra como lidar com entradas e saídas ao usar o Python no SQL Server Serviços de Machine Learning.

Por padrão, o [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) aceita um único conjunto de dados de entrada, que normalmente você fornece na forma de uma consulta SQL válida.

Outros tipos de entrada podem ser passados como variáveis SQL: por exemplo, você pode passar um modelo treinado como uma variável, usando uma função de serialização como [pickle](https://docs.python.org/3.0/library/pickle.html) ou [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) para gravar o modelo em um formato binário.

O procedimento armazenado retorna um único quadro de dados do Python [pandas](https://pandas.pydata.org/pandas-docs/stable/index.html) como saída, mas você também pode gerar escalares e modelos como variáveis. Por exemplo, você pode gerar um modelo treinado como uma variável binária e passá-lo para uma instrução T-SQL INSERT, para gravar esse modelo em uma tabela. Você também pode gerar plotagens (em formato binário) ou escalares (valores individuais, como a data e hora, o tempo decorrido para treinar o modelo e assim por diante).

## <a name="prerequisites"></a>Pré-requisitos

Um guia de início rápido anterior, [Verifique se o Python existe no SQL Server](quickstart-python-verify.md), fornece informações e links para configurar o ambiente do Python necessário para este guia de início rápido.

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

Vejamos as variáveis de entrada e saída padrão de sp_execute_external_script: `InputDataSet` e. `OutputDataSet`

1. Você pode obter os dados da tabela como entrada para o script Python. Execute a instrução abaixo. Ele obtém os dados da tabela, faz uma viagem de ida e volta pelo tempo de execução do Python e retorna os valores com o nome da coluna *NewColName*.

    Os dados retornados pela consulta são passados para o tempo de execução do Python, que retorna os dados para o SQL Database como um dataframe do pandas. A cláusula com conjuntos de resultados define o esquema da tabela de dados retornada para o banco de dado SQL.

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'Python'
        , @script = N'OutputDataSet = InputDataSet;'
        , @input_data_1 = N'SELECT * FROM PythonTestData;'
    WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    **Resultados**

    ![Saída do script Python que retorna dados de uma tabela](./media/python-output-pythontestdata.png)

2. Vamos alterar o nome das variáveis de entrada ou saída. O script acima usou os nomes de variáveis de entrada e saída padrão, _InputDataSet_ e _OutputDataSet_. Para definir os dados de entrada associados ao _InputDataSet_, use a *@input_data_1* variável.

    Nesse script, os nomes das variáveis de saída e de entrada para o procedimento armazenado foram alterados para *SQL_out* e *SQL_in*:

    ```sql
    EXECUTE sp_execute_external_script
      @language = N'Python'
      , @script = N'SQL_out = SQL_in'
      , @input_data_1 = N' SELECT 12 as Col;'
      , @input_data_1_name  = N'SQL_in'
      , @output_data_1_name =  N'SQL_out'
      WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    O caso das variáveis de entrada e saída no `@input_data_1_name` e `@output_data_1_name` precisam corresponder ao caso daqueles no código Python no `@script`, pois o Python diferencia maiúsculas de minúsculas.

    Apenas um conjunto de dados de entrada pode ser passado como um parâmetro e é possível retornar apenas um conjunto de dados. No entanto, você pode chamar outros conjuntos de resultados de dentro de seu código Python e pode retornar saídas de outros tipos além do conjunto de um. Você também pode adicionar a palavra-chave OUTPUT a qualquer parâmetro para que ele seja retornado com os resultados. 

    A `WITH RESULT SETS` instrução define o esquema para os dados que são usados em SQL Server. Você precisa fornecer tipos de dados compatíveis com SQL para cada coluna retornada do Python. Você pode usar a definição de esquema para fornecer novos nomes de coluna também, já que não é necessário usar os nomes de coluna do Python Data. frame.

3. Você também pode gerar valores usando o script Python e deixar a cadeia de caracteres de _@input_data_1_ consulta de entrada em branco.

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

    ![Resultados da consulta @script usando como entrada](./media/python-data-generated-output.png)

## <a name="next-steps"></a>Próximas etapas

Examine alguns dos problemas que você pode encontrar ao passar dados tabulares entre Python e SQL Server.

> [!div class="nextstepaction"]
> [Início Rápido: Estruturas de dados do Python no SQL Server](quickstart-python-data-structures.md)
