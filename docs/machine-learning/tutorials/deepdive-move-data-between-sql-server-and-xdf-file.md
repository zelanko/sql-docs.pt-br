---
title: Mover dados com o arquivo XDF
description: 'Tutorial 13 do RevoScaleR: Como mover dados usando o XDF e a linguagem R no SQL Server.'
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9c7e5ce4cbe995fd677acd406187dfaf264a7461
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85680007"
---
# <a name="move-data-between-sql-server-and-xdf-file-sql-server-and-revoscaler-tutorial"></a>Mover dados entre o SQL Server e o arquivo XDF (Tutorial do SQL Server e RevoScaleR)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Este é o tutorial 13 da [série de tutoriais do RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar as [funções do RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Neste tutorial, você aprenderá a usar um arquivo XDF para transferir dados entre os contextos de computação locais e remotos. Armazenar os dados em um arquivo XDF permite que você execute transformações nos dados.

Quando terminar, você usará os dados no arquivo para criar uma tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A função [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) pode aplicar transformações aos dados e executar a conversão entre quadros de dados e arquivos .xdf.
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>Criar uma tabela do SQL Server com base em um arquivo XDF

Para este exercício, use os dados de fraude de cartão de crédito novamente. Nesse cenário, foi solicitado que você fizesse algumas análises adicionais nos usuários nos Estados da Califórnia, Oregon e Washington. Para ser mais eficiente, você decidiu armazenar dados apenas desses estados no computador local e trabalhar apenas com as variáveis gender, cardholder, state e balance.

1. Use novamente a variável `stateAbb` criada anteriormente para identificar os níveis a serem incluídos e grave-os em uma nova variável, `statesToKeep`.
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **Resultados**
    
    CA|OU|WA
    ----|----|----
    5|38|48
    
2. Defina os dados que deseja trazer do SQL Server usando uma consulta [!INCLUDE[tsql](../../includes/tsql-md.md)].  Posteriormente, use essa variável como o argumento *inData* para **rxImport**.
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    Verifique se não há caracteres ocultos, como tabulações ou alimentações de linha.
  
3. Em seguida, defina as colunas a serem usadas ao trabalhar com os dados no R. Por exemplo, no conjunto de dados menor, você precisa ter apenas três níveis de fator, porque a consulta retorna dados de apenas três estados.  Aplique a variável `statesToKeep` para identificar os níveis corretos a serem incluídos.
  
    ```R
    importColInfo <- list(
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))
            )
    ```
  
4. Defina o contexto de computação como **local**, porque você deseja ter todos os dados disponíveis no computador local.
  
    ```R
    rxSetComputeContext("local")
    ```
    
    A função [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) pode importar dados de qualquer fonte de dados com suporte para um arquivo XDF local. Usar uma cópia local dos dados é conveniente quando você deseja realizar muitas análises diferentes nos dados, mas deseja evitar a execução da mesma consulta repetidamente.

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
  
    O objeto `localDs` retornado pela função **rxImport** é um objeto de fonte de dados **RxXdfData** leve que representa o arquivo de dados `ccFraud.xdf` armazenado localmente em disco.
  
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

8. Agora, você pode chamar várias funções do R para analisar o objeto **localDs**, como faria com os dados de origem no SQL Server. Por exemplo, você pode resumir pelo gender:
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

## <a name="next-steps"></a>Próximas etapas

Esse tutorial conclui a série de tutoriais de várias partes sobre **RevoScaleR** e SQL Server. Ela apresentou vários conceitos de computação e relacionados a dados, oferecendo uma base para avançar com seus próprios dados e requisitos de projeto.

Para aprofundar seu conhecimento sobre o **RevoScaleR**, você pode voltar para a lista de tutoriais do R para percorrer os exercícios que você possa ter perdido. Como alternativa, examine os artigos de instruções no sumário para obter informações sobre tarefas gerais.

> [!div class="nextstepaction"]
> [Tutoriais de R para SQL Server](sql-server-r-tutorials.md)