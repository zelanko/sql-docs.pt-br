---
title: Início rápido para trabalhar com entradas e saídas em R
description: Neste guia de início rápido para o script R no SQL Server, saiba como estruturar entradas e saídas para o procedimento armazenado do sistema sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 75de63ef960c205545db5229f22a437c70b350b9
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714791"
---
# <a name="quickstart-handle-inputs-and-outputs-using-r-in-sql-server"></a>Início Rápido: Manipular entradas e saídas usando R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este guia de início rápido mostra como lidar com entradas e saídas ao usar o R em SQL Server Serviços de Machine Learning ou R Services.

Quando você quiser executar o código R no SQL Server, deverá encapsular o script R em um procedimento armazenado. Você pode escrever um ou passar o script R para [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Esse procedimento armazenado do sistema é usado para iniciar o tempo de execução do R no contexto de SQL Server, que passa dados para o R, gerencia as sessões de usuário do R com segurança e retorna todos os resultados para o cliente.

Por padrão, o [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) aceita um único conjunto de dados de entrada, que normalmente você fornece na forma de uma consulta SQL válida. Outros tipos de entrada podem ser passados como variáveis SQL.

O procedimento armazenado retorna um único quadro de dados do R como saída, mas você também pode gerar escalares e modelos como variáveis. Por exemplo, você pode gerar um modelo treinado como uma variável binária e passá-lo para uma instrução T-SQL INSERT, para gravar esse modelo em uma tabela. Você também pode gerar plotagens (em formato binário) ou escalares (valores individuais, como a data e hora, o tempo decorrido para treinar o modelo e assim por diante).

## <a name="prerequisites"></a>Pré-requisitos

Um guia de início rápido anterior, [verificar se o R existe no SQL Server](quickstart-r-verify.md), fornece informações e links para configurar o ambiente de R necessário para este guia de início rápido.

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

Vejamos as variáveis de entrada e saída padrão de sp_execute_external_script: `InputDataSet` e. `OutputDataSet`

1. Você pode obter os dados da tabela como entrada para o script R. Execute a instrução abaixo. Ele obtém os dados da tabela, faz uma viagem de ida e volta pelo tempo de execução de R e retorna os valores com o nome de coluna *NewColName*.

    Os dados retornados pela consulta são passados para o tempo de execução de R, que retorna os dados para o banco de dados SQL como um quadro de dado. A cláusula com conjuntos de resultados define o esquema da tabela de dados retornada para o banco de dado SQL.

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    **Resultados**

    ![Saída do script R que retorna dados de uma tabela](./media/r-output-rtestdata.png)

2. Vamos alterar o nome das variáveis de entrada ou saída. O script acima usou os nomes de variáveis de entrada e saída padrão, _InputDataSet_ e _OutputDataSet_. Para definir os dados de entrada associados ao _InputDatSet_, use a *@input_data_1* variável.

    Nesse script, os nomes das variáveis de saída e de entrada para o procedimento armazenado foram alterados para *SQL_out* e *SQL_in*:

    ```sql
    EXECUTE sp_execute_external_script
      @language = N'R'
      , @script = N' SQL_out <- SQL_in;'
      , @input_data_1 = N'SELECT 12 as Col;'
      , @input_data_1_name  = N'SQL_in'
      , @output_data_1_name =  N'SQL_out'
      WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    Observe que o R diferencia maiúsculas de minúsculas, portanto, o caso das variáveis de `@input_data_1_name` entrada `@output_data_1_name` e saída no e precisa corresponder àquelas no código `@script`R no. 

    Apenas um conjunto de dados de entrada pode ser passado como um parâmetro e é possível retornar apenas um conjunto de dados. No entanto, você pode chamar outros conjuntos de dados no código do R e retornar saídas de outros tipos, além do conjunto de dados. Você também pode adicionar a palavra-chave OUTPUT a qualquer parâmetro para que ele seja retornado com os resultados. 

    A `WITH RESULT SETS` instrução define o esquema para os dados que são usados em SQL Server. Você precisa fornecer tipos de dados compatíveis com SQL para cada coluna retornada do R. Você pode usar a definição de esquema para fornecer novos nomes de coluna também, pois não é necessário usar os nomes de coluna do quadro de dados do R.

3. Você também pode gerar valores usando o script R e deixar a cadeia de caracteres de _@input_data_1_ consulta de entrada em branco.

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'R'
        , @script = N' mytextvariable <- c("hello", " ", "world");
            OutputDataSet <- as.data.frame(mytextvariable);'
        , @input_data_1 = N''
    WITH RESULT SETS (([Col1] CHAR(20) NOT NULL));
    ```

    **Resultados**

    ![Resultados da consulta @script usando como entrada](./media/r-data-generated-output.png)

## <a name="next-steps"></a>Próximas etapas

Examine alguns dos problemas que você pode encontrar ao passar dados entre R e SQL Server, como conversões implícitas e diferenças em dados tabulares entre R e SQL.

> [!div class="nextstepaction"]
> [Início Rápido: Manipular tipos de dados e objetos](quickstart-r-data-types-and-objects.md)