---
title: Mover dados entre SQL Server e arquivo XDF usando RevoScaleR
description: Tutorial explicativo sobre como mover dados usando o XDF e a linguagem R em SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7eb32a6ba915328a7f6a6baccdc948f534da1a09
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715555"
---
# <a name="move-data-between-sql-server-and-xdf-file-sql-server-and-revoscaler-tutorial"></a>Mover dados entre SQL Server e arquivo XDF (tutorial SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Esta lição faz parte do [tutorial do RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar as [funções do RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com SQL Server.

Nesta etapa, aprenda a usar um arquivo XDF para transferir dados entre os contextos de computação locais e remotos. Armazenar os dados em um arquivo XDF permite que você execute transformações nos dados.

Quando terminar, você usará os dados no arquivo para criar uma nova [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela. A função [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) pode aplicar transformações aos dados e executa a conversão entre quadros de dados e arquivos. Xdf.
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>Criar uma tabela de SQL Server de um arquivo XDF

Para este exercício, você usará os dados de fraude de cartão de crédito novamente. Nesse cenário, foi solicitado que você fizesse algumas análises adicionais nos usuários nos Estados da Califórnia, Oregon e Washington. Para ser mais eficiente, você decidiu armazenar dados somente para esses Estados em seu computador local e trabalhar apenas com as variáveis gênero, titular do cartão, estado e saldo.

1. Use novamente a `stateAbb` variável que você criou anteriormente para identificar os níveis a serem incluídos e gravá-los em uma nova variável `statesToKeep`,.
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **Resultados**
    
    CA|OU|WA
    ----|----|----
    5|38|48
    
2. Defina os dados que você deseja trazer de SQL Server, usando uma [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta.  Posteriormente, você usará essa variável como o argumento Indata para **rxImport**.
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    Verifique se não há caracteres ocultos, como tabulações ou alimentações de linha.
  
3. Em seguida, defina as colunas a serem usadas ao trabalhar com os dados em R. Por exemplo, no conjunto de dados menor, você precisa de apenas três níveis de fator, porque a consulta retorna dados apenas para três Estados.  Aplique a `statesToKeep` variável para identificar os níveis corretos a serem incluídos.
  
    ```R
    importColInfo <- list(
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))
            )
    ```
  
4. Defina o contexto de computação como **local**, pois você deseja que todos os dados estejam disponíveis no computador local.
  
    ```R
    rxSetComputeContext("local")
    ```
    
    A função [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) pode importar dados de qualquer fonte de dados com suporte para um arquivo Xdf local. Usar uma cópia local dos dados é conveniente quando você deseja fazer muitas análises diferentes nos dados, mas deseja evitar executar a mesma consulta repetidamente.

5. Crie o objeto de fonte de dados passando as variáveis definidas anteriormente como argumentos para **RxSqlServerData**.
  
    ```R
    sqlServerImportDS <- RxSqlServerData(
        connectionString = sqlConnString,
        sqlQuery = importQuery,
        colInfo = importColInfo)
    ```
  
6. Chame **rxImport** para gravar os dados em um arquivo chamado `ccFraudSub.xdf`, no diretório de trabalho atual.
  
    ```R
    localDS <- rxImport(inData = sqlServerImportDS,
        outFile = "ccFraudSub.xdf",
        overwrite = TRUE)
    ```
  
    O `localDs` objeto retornado pela função **rxImport** é um objeto de fonte de dados **RxXdfData** leve que representa o arquivo `ccFraud.xdf` de dados armazenado localmente no disco.
  
7. Chame [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) no arquivo XDF para verificar se o esquema de dados é o mesmo.
  
    ```R
    rxGetVarInfo(data = localDS)
    ```

    **Resultados**
    
    ```R
    rxGetVarInfo(data = localDS)
    Var 1: gender, Type: factor, no factor levels available
    Var 2: cardholder, Type: factor, no factor levels available
    Var 3: balance, Type: integer, Low/High: (0, 22463)
    Var 4: state, Type: factor, no factor levels available
    ```

8. Agora você pode chamar várias funções do R para analisar o objeto **localDs** , assim como faria com os dados de origem em SQL Server. Por exemplo, você pode resumir por gênero:
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

## <a name="next-steps"></a>Próximas etapas

Esta lição conclui a série de tutoriais de várias partes em **RevoScaleR** e SQL Server. Ele apresentou a você vários conceitos de computação e de dados, oferecendo a você uma base para avançar com seus próprios dados e requisitos de projeto.

Para aprofundar seu conhecimento sobre o **RevoScaleR**, você pode retornar à lista de tutoriais do R para percorrer todos os exercícios que você possa ter perdido. Como alternativa, examine os artigos de instruções no sumário para obter informações sobre tarefas gerais.

> [!div class="nextstepaction"]
> [Tutoriais de R para SQL Server](sql-server-r-tutorials.md)