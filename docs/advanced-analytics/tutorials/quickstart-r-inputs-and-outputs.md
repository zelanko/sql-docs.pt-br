---
title: Guia de início rápido para trabalhar com entradas e saídas em R - aprendizagem de máquina do SQL Server
description: Neste início rápido para o script de R no SQL Server, saiba como estruturar as entradas e saídas para o procedimento armazenado do sistema de sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 1672cdeb59dfe35e313c999549e46f3fd76b688e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962009"
---
# <a name="quickstart-handle-inputs-and-outputs-using-r-in-sql-server"></a>Início Rápido: Lidar com entradas e saídas usando o R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Neste início rápido mostra como lidar com entradas e saídas ao usar R em serviços do SQL Server Machine Learning ou R Services.

Quando você deseja executar o código R no SQL Server, você deve encapsular o script R em um procedimento armazenado. Você pode escrever uma ou passar o script R à [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Esse sistema de procedimento armazenado é usado para iniciar o tempo de execução de R no contexto do SQL Server, que transmite dados para R, gerencia as sessões de usuário de R com segurança e retorna todos os resultados ao cliente.

Por padrão, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) aceita um único conjunto de dados entrado, que normalmente você fornece na forma de uma consulta SQL válida. Outros tipos de entrada podem ser passados como variáveis SQL.

O procedimento armazenado retorna um único quadro de dados de R como saída, mas você também pode gerar modelos como variáveis e escalares. Por exemplo, você pode gerar um modelo treinado como uma variável binária e passá-lo para uma instrução T-SQL INSERT, para gravar esse modelo em uma tabela. Você também pode gerar plotagens (em formato binário) ou escalares (valores individuais, como a data e hora, o tempo decorrido para treinar o modelo e assim por diante).

## <a name="prerequisites"></a>Pré-requisitos

Um início rápido anterior, [R Verifique se existe no SQL Server](quickstart-r-verify.md), fornece informações e links para configurar o ambiente de R necessários para este início rápido.

## <a name="create-the-source-data"></a>Criar os dados de origem

Crie uma pequena tabela de dados de teste executando a seguinte instrução T-SQL:

```sql
CREATE TABLE RTestData (col1 INT NOT NULL)
INSERT INTO RTestData VALUES (1);
INSERT INTO RTestData VALUES (10);
INSERT INTO RTestData VALUES (100);
GO
```

Assim que a tabela tiver sido criada, use a seguinte instrução para consultar a tabela:
  
```sql
SELECT * FROM RTestData
```

**Resultados**

![Conteúdo da tabela RTestData](./media/select-rtestdata.png)

## <a name="inputs-and-outputs"></a>Entradas e Saídas

Vamos dar uma olhada no padrão variáveis de entrada e saídas de sp_execute_external_script: `InputDataSet` e `OutputDataSet`.

1. Você pode obter os dados da tabela como entrada para seu script R. Execute a instrução a seguir. Obtém os dados da tabela, faz uma viagem de ida e por meio de execução R e retornar os valores com o nome da coluna *NewColName*.

    Os dados retornados pela consulta são passados para o tempo de execução de R, que retorna os dados ao banco de dados SQL como um quadro de dados. A cláusula WITH RESULT SETS define o esquema da tabela de dados retornados para o banco de dados SQL.

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    **Resultados**

    ![Saída do script R que retorna dados de uma tabela](./media/r-output-rtestdata.png)

2. Vamos alterar o nome das variáveis de entrada ou saídas. O script acima usado o padrão de entrada e saída de nomes de variáveis _InputDataSet_ e _OutputDataSet_. Para definir os dados de entrada associados _InputDatSet_, você usa o *@input_data_1* variável.

    Nesse script, os nomes das variáveis de entrada e saída para o procedimento armazenado foi alterados para *SQL_out* e *SQL_in*:

    ```sql
    EXECUTE sp_execute_external_script
      @language = N'R'
      , @script = N' SQL_out <- SQL_in;'
      , @input_data_1 = N'SELECT 12 as Col;'
      , @input_data_1_name  = N'SQL_in'
      , @output_data_1_name =  N'SQL_out'
      WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    Observe que o R diferencia maiusculas de minúsculas, portanto, o caso das variáveis de entrada e saídas no `@input_data_1_name` e `@output_data_1_name` precisa coincidir com aqueles no código R em `@script`. 

    Apenas um conjunto de dados de entrada pode ser passado como um parâmetro e é possível retornar apenas um conjunto de dados. No entanto, você pode chamar outros conjuntos de dados no código do R e retornar saídas de outros tipos, além do conjunto de dados. Você também pode adicionar a palavra-chave OUTPUT a qualquer parâmetro para que ele seja retornado com os resultados. 

    O `WITH RESULT SETS` instrução define o esquema para os dados que são usados no SQL Server. Você precisa fornecer tipos de dados compatíveis do SQL para cada coluna retornada do R. Você pode usar a definição de esquema para fornecer novos nomes de coluna muito, pois você não precisará usar os nomes de coluna do quadro de dados de R.

3. Você também pode gerar valores usando o script de R e deixar a cadeia de caracteres de consulta de entrada em _@input_data_1_ em branco.

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'R'
        , @script = N' mytextvariable <- c("hello", " ", "world");
            OutputDataSet <- as.data.frame(mytextvariable);'
        , @input_data_1 = N''
    WITH RESULT SETS (([Col1] CHAR(20) NOT NULL));
    ```

    **Resultados**

    ![Os resultados da consulta usando @script como entrada](./media/r-data-generated-output.png)

## <a name="next-steps"></a>Próximas etapas

Examine alguns dos problemas que podem ocorrer ao passar dados entre R e SQL Server, como conversões implícitas e diferenças de dados tabulares entre R e SQL.

> [!div class="nextstepaction"]
> [Início Rápido: Lidar com tipos de dados e objetos](quickstart-r-data-types-and-objects.md)