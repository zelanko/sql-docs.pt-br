---
title: Mover dados entre o SQL Server e o arquivo XDF usando o RevoScaleR - aprendizagem de máquina do SQL Server
description: Tutorial passo a passo sobre como mover dados usando o XDF e a linguagem R no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 40852f62cc985f300d04eac4dbef5810f823e124
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512303"
---
# <a name="move-data-between-sql-server-and-xdf-file-sql-server-and-revoscaler-tutorial"></a>Mover dados entre o SQL Server e o arquivo XDF (tutorial do SQL Server e o RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Esta lição é parte do [tutorial de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar [funções RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Nesta etapa, Aprenda a usar um arquivo XDF para transferir dados entre contextos de computação local e remoto. Armazenar os dados em um arquivo XDF permite executar transformações nos dados.

Quando você terminar de usar os dados no arquivo para criar um novo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela. A função [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) pode aplicar transformações aos dados e executa a conversão entre os quadros de dados e arquivos. xdf.
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>Criar uma tabela do SQL Server de um arquivo XDF

Para este exercício, use os dados de fraude de cartão de crédito novamente. Nesse cenário, foi solicitado que você fizesse algumas análises adicionais nos usuários nos Estados da Califórnia, Oregon e Washington. Para ser mais eficiente, você decidiu armazenar dados para apenas esses estados em seu computador local e trabalhar com apenas as variáveis gender, do titular do cartão, estado e saldo.

1. Use novamente o `stateAbb` variável que você criou anteriormente para identificar os níveis para incluir e gravá-las em uma nova variável, `statesToKeep`.
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **Resultados**
    
    CA|OU|WA
    ----|----|----
    5|38|48
    
2. Definir os dados que você deseja trazer do SQL Server, usando um [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta.  Mais tarde você pode usar essa variável como o *inData* argumento para **rxImport**.
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    Verifique se não há caracteres ocultos, como tabulações ou alimentações de linha.
  
3. Em seguida, defina as colunas a serem usadas ao trabalhar com os dados em R. Por exemplo, no conjunto de dados menor, você precisa apenas três níveis de fator, porque a consulta retorna dados de apenas três estados.  Aplicar o `statesToKeep` variável para identificar os níveis corretos a serem incluídos.
  
    ```R
    importColInfo <- list(
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))
            )
    ```
  
4. Definir o contexto de computação para **local**, porque você deseja que todos os dados disponíveis no computador local.
  
    ```R
    rxSetComputeContext("local")
    ```
    
    O [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) função pode importar dados de qualquer fonte de dados com suporte em um arquivo XDF local. Usar uma cópia local dos dados é conveniente quando você deseja fazer várias análises diferentes nos dados, mas deseja evitar executar a mesma consulta repetidamente.

5. Criar o objeto de fonte de dados, passando as variáveis definidas anteriormente como argumentos para **RxSqlServerData**.
  
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
  
    O `localDs` objeto retornado pela **rxImport** função é um leve **RxXdfData** objeto de fonte de dados que representa o `ccFraud.xdf` arquivo de dados armazenados localmente no disco.
  
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

8. Agora você pode chamar várias funções de R para analisar a **localDs** do objeto, assim como faria com dados de origem no SQL Server. Por exemplo, você pode resumir por gênero:
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

## <a name="next-steps"></a>Próximas etapas

Esta lição conclui a série de tutoriais de várias parte no **RevoScaleR** e o SQL Server. Ele apresentou vários conceitos computacionais e dados relacionados, dando a você uma base para avançar com seus próprios requisitos de projeto e de dados.

Para aprofundar seu conhecimento de **RevoScaleR**, você pode retornar à lista de tutoriais de R para percorrer qualquer exercícios que você pode ter perdido. Como alternativa, examine os artigos de instrução na tabela de conteúdo para obter informações sobre tarefas gerais.

> [!div class="nextstepaction"]
> [Tutoriais de R para SQL Server](sql-server-r-tutorials.md)