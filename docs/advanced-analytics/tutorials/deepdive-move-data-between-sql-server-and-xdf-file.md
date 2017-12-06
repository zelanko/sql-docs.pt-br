---
title: Mover dados entre o SQL Server e o arquivo XDF | Microsoft Docs
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 40887cb3-ffbb-4769-9f54-c006d7f4798c
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a140cc358afab1f1ff324e0a47ed67501ee75e23
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2017
---
# <a name="move-data-between-sql-server-and-xdf-file"></a>Mover dados entre o SQL Server e o arquivo XDF

Quando você estiver trabalhando em um contexto de computação local, você tem acesso a ambos os arquivos de dados local e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (definido como uma fonte de dados RxSqlServerData) do banco de dados.

Nesta seção, você aprenderá a obter dados e armazená-los em um arquivo no computador local para que possa executar transformações nos dados. Quando terminar, você usará os dados no arquivo para criar um novo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela, usando rxDataStep.
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>Criar uma tabela do SQL Server com base em um arquivo XDF

A função rxImport permite importar dados de qualquer fonte de dados com suporte para um arquivo XDF local. Usar um arquivo local poderá ser conveniente se você desejar fazer várias análises diferentes dos dados armazenados em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e quiser evitar executar a mesma consulta repetidamente.

Para este exercício, você usará os dados de fraude de cartão de crédito novamente. Nesse cenário, foi solicitado que você fizesse algumas análises adicionais nos usuários nos Estados da Califórnia, Oregon e Washington. Para ser mais eficiente, você decidiu armazenar dados apenas desses estados no computador local e trabalhar com as variáveis gender, cardholder, state e balance.

1. Use novamente o vetor *stateAbb* criado anteriormente para identificar os níveis a serem incluídos e imprima a nova variável, *statesToKeep*, no console.
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **Resultados**
    
    CA|OU|WA
    ----|----|----
    5|38|48
    
2. Agora, você definirá os dados que deseja trazer do SQL Server usando uma consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] .  Posteriormente, você usará essa variável como o argumento *inData* para *rxImport*.
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    Verifique se não há caracteres ocultos, como tabulações ou alimentações de linha.
  
3. Em seguida, você definirá as colunas a serem usadas ao trabalhar com os dados em R. Por exemplo, no conjunto de dados menor, você precisa apenas três níveis de fator, porque a consulta retornará dados para somente três estados.  Você pode utilizar a variável *statesToKeep* novamente para identificar os níveis corretos a serem incluídos.
  
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
  
5. Crie o objeto de fonte de dados, passando a todas as variáveis que você acabou de definir como argumentos para RxSqlServerData.
  
    ```R
    sqlServerImportDS <- RxSqlServerData(
        connectionString = sqlConnString,
        sqlQuery = importQuery,
        colInfo = importColInfo)
    ```
  
6. Em seguida, chame **rxImport** para gravar os dados em um arquivo chamado `ccFraudSub.xdf`, no diretório de trabalho atual.
  
    ```R
    localDS <- rxImport(inData = sqlServerImportDS,
        outFile = "ccFraudSub.xdf",
        overwrite = TRUE)
    ```
  
    O *localDs* objeto retornado pela função rxImport é um objeto de fonte de dados de RxXdfData leve que representa o arquivo de dados ccFraud.xdf armazenado localmente no disco.
  
7. Chamada à função rxGetVarInfo no arquivo XDF para verificar se o esquema de dados é o mesmo.
  
    ```R
    rxGetVarInfo(data = localDS)
    ```

    **Resultados**
    
    *rxGetVarInfo(data = localDS)*

    *Var 1: gender, Type: factor, no factor levels available*

    *Var 2: cardholder, Type: factor, no factor levels available*

    *Var 3: balance, Type: integer, Low/High: (0, 22463)*

    *Var 4: state, Type: factor, no factor levels available*
  
8. Agora, você pode chamar várias funções do R para analisar o objeto *localDs* , da mesma forma como faria com dados de origem no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por exemplo:
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

Agora que você já dominou o uso de contextos de computação e o trabalho com várias fontes de dados, é hora de experimentar algo divertido. Na próxima e última lição, você criará uma simulação simples usando uma função personalizada do R e a executará no servidor remoto.

## <a name="next-step"></a>Próxima etapa

[Criar um simples de simulação](../../advanced-analytics/tutorials/deepdive-create-a-simple-simulation.md)

## <a name="previous-step"></a>Etapa anterior

[Analisar dados no contexto de computação Local](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)



