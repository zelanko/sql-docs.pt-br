---
title: Mover dados entre o SQL Server e o arquivo XDF (SQL e R mergulho profundo) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6eb2ed7bdda7fab662048d7e8da692253cf9c164
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="move-data-between-sql-server-and-xdf-file-sql-and-r-deep-dive"></a>Mover dados entre o SQL Server e o arquivo XDF (SQL e R mergulho profundo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo faz parte do tutorial mergulho profundo de ciência de dados, como usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Nesta etapa, você aprenderá a usar um arquivo XDF para transferir dados entre os contextos de computação local e remoto. Armazenar os dados em um arquivo XDF permite realizar transformações nos dados.

Quando terminar, você usar os dados no arquivo para criar um novo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela. A função [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) pode aplicar transformações aos dados e executa a conversão entre os quadros de dados e arquivos. xdf.
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>Criar uma tabela do SQL Server de um arquivo XDF

Para este exercício, você usar os dados de fraude de cartão de crédito novamente. Nesse cenário, foi solicitado que você fizesse algumas análises adicionais nos usuários nos Estados da Califórnia, Oregon e Washington. Para ser mais eficiente, você decidir armazenar dados para apenas esses estados em seu computador local, e trabalhar com apenas o sexo de variáveis, titular do cartão, estado e equilíbrio.

1. Usar novamente o `stateAbb` variável que você criou anteriormente para identificar os níveis para incluir e gravá-las em uma nova variável, `statesToKeep`.
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **Resultados**
    
    CA|OU|WA
    ----|----|----
    5|38|48
    
2. Definir os dados que você quer fazer do SQL Server, usando um [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta.  Mais tarde você pode usar essa variável como o *inData* argumento **rxImport**.
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    Verifique se não há caracteres ocultos, como tabulações ou alimentações de linha.
  
3. Em seguida, definir colunas a serem usadas ao trabalhar com os dados em R. Por exemplo, no conjunto de dados menor, você precisa apenas três níveis de fator, pois a consulta retorna os dados para somente três estados.  Aplicar o `statesToKeep` variável para identificar os níveis corretos para incluir.
  
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
    
    O [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) função pode importar dados de qualquer fonte de dados com suporte para um arquivo XDF local. Usando uma cópia local dos dados é conveniente quando você deseja fazer muitas análises diferentes nos dados, mas queira evitar executar a mesma consulta repetidamente.

5. Criar o objeto de fonte de dados, passando as variáveis definidas anteriormente como argumentos para **RxSqlServerData**.
  
    ```R
    sqlServerImportDS <- RxSqlServerData(
        connectionString = sqlConnString,
        sqlQuery = importQuery,
        colInfo = importColInfo)
    ```
  
6. Chamar **rxImport** para gravar os dados em um arquivo chamado `ccFraudSub.xdf`, no diretório de trabalho atual.
  
    ```R
    localDS <- rxImport(inData = sqlServerImportDS,
        outFile = "ccFraudSub.xdf",
        overwrite = TRUE)
    ```
  
    O `localDs` objeto retornado pelo **rxImport** função é um leve **RxXdfData** objeto de fonte de dados que representa o `ccFraud.xdf` arquivo de dados armazenados localmente no disco.
  
7. Chame [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) no arquivo XDF para verificar se o esquema de dados é o mesmo.
  
    ```R
    rxGetVarInfo(data = localDS)
    ```

    **Resultados**
    
    *rxGetVarInfo(data = localDS)*

    *Var 1: gender, Type: factor, no factor levels available*

    *Var 2: cardholder, Type: factor, no factor levels available*

    *Var 3: balance, Type: integer, Low/High: (0, 22463)*

    *Var 4: state, Type: factor, no factor levels available*
  
8. Agora você pode chamar várias funções do R para analisar o objeto `localDs`, da mesma forma como faria com dados de origem no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por exemplo, você pode resumir por gênero:
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

Agora que você já dominou o uso de contextos de computação e o trabalho com várias fontes de dados, é hora de experimentar algo divertido. A lição final e Avançar, você criará uma simulação simple que executa uma função personalizada do R no servidor remoto.

## <a name="next-step"></a>Próxima etapa

[Criar uma simulação simples](../../advanced-analytics/tutorials/deepdive-create-a-simple-simulation.md)

## <a name="previous-step"></a>Etapa anterior

[Analisar dados no contexto de computação local](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)



