---
title: "Mover dados entre o SQL Server e o arquivo XDF (Aprofundamento da ci&#234;ncia de dados) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 40887cb3-ffbb-4769-9f54-c006d7f4798c
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Mover dados entre o SQL Server e o arquivo XDF (Aprofundamento da ci&#234;ncia de dados)
Quando estiver trabalhando em um contexto de computação local, você tem acesso aos arquivos de dados locais e ao banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (definido como uma fonte de dados *RxSqlServerData*).  
  
Nesta seção, você aprenderá a obter dados e armazená-los em um arquivo no computador local para que possa executar transformações nos dados. Quando terminar, você usará os dados no arquivo para criar uma nova tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], usando *rxDataStep*.  
  
## Criar uma tabela do SQL Server com base em um arquivo XDF  

A função *rxImport* permite importar dados de qualquer fonte de dados com suporte para um arquivo XDF local. Usar um arquivo local poderá ser conveniente se você desejar fazer várias análises diferentes dos dados armazenados em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e quiser evitar executar a mesma consulta repetidamente.  
  
Para este exercício, você usará os dados de fraude de cartão de crédito novamente. Nesse cenário, foi solicitado que você fizesse algumas análises adicionais nos usuários nos Estados da Califórnia, Oregon e Washington. Para ser mais eficiente, você decidiu armazenar dados apenas desses estados no computador local e trabalhar com as variáveis gender, cardholder, state e balance.  
  
1.  Use novamente o vetor *stateAbb* criado anteriormente para identificar os níveis a serem incluídos e imprima a nova variável, *statesToKeep*, no console.  
  
    ```  
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)   
  
    statesToKeep  
  
    ```  
 **Resultados**
CA |  OU  | WA 
-- | -- | --
 5 |  38  | 48 
  
2.  Agora, você definirá os dados que deseja trazer do SQL Server usando uma consulta [!INCLUDE[tsql](../../includes/tsql-md.md)].  Posteriormente, você usará essa variável como o argumento *inData* para *rxImport*.  
  
    ```R  
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")  
  
    ```  
  
    Verifique se não há caracteres ocultos, como tabulações ou alimentações de linha.  
  
3.  Em seguida, você definirá as colunas a serem usadas quando trabalhar com dados em R.  
  Por exemplo, no conjunto de dados menor, você precisa ter apenas três níveis de fator, porque a consulta retornará dados de apenas três estados.  Você pode utilizar a variável *statesToKeep* novamente para identificar os níveis corretos a serem incluídos.  
  
    ```R  
    importColInfo <- list(   
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),       
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),     
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))   
            )  
  
    ```  
  
4.  Defina o contexto de computação como **local**, porque você deseja ter todos os dados disponíveis no computador local.  
  
    ```R  
    rxSetComputeContext("local")   
    ```  
  
5.  Crie o objeto de fonte de dados passando todas as variáveis que você acabou de definir como argumentos para *RxSqlServerData*.  
  
    ```R  
    sqlServerImportDS <- RxSqlServerData(  
        connectionString = sqlConnString,   
        sqlQuery = importQuery,   
        colInfo = importColInfo)  
  
    ```  
  
6.  Em seguida, chame *rxImport* para salvar os dados no diretório de trabalho atual, em um arquivo chamado `ccFraudSub.xdf`.  
  
    ```R  
    localDS <- rxImport(inData = sqlServerImportDS,   
        outFile = "ccFraudSub.xdf",    
        overwrite = TRUE)  
  
    ```  
  
    O objeto *localDs* retornado pela função *rxImport* é um objeto de fonte de dados *RxXdfData* leve que representa o arquivo de dados ccFraud.xdf armazenado localmente em disco.  
  
7.  Chame *rxGetVarInfo* no arquivo XDF para verificar se o esquema de dados é o mesmo.  
  
    ```R  
    rxGetVarInfo(data = localDS)   
    ```  
    **Resultados**
    
    *rxGetVarInfo(data = localDS)*    
    *Var 1: gender, Type: factor, no factor levels available*    
    *Var 2: cardholder, Type: factor, no factor levels available*    
    *Var 3: balance, Type: integer, Low/High: (0, 22463)*    
    *Var 4: state, Type: factor, no factor levels available*
  
8.  Agora, você pode chamar várias funções do R para analisar o objeto *localDs*, da mesma forma como faria com dados de origem no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por exemplo:  
  
    ```R  
    rxSummary(~gender + cardholder + balance + state, data = localDS)    
    ```  
  
Agora que você já dominou o uso de contextos de computação e o trabalho com várias fontes de dados, é hora de experimentar algo divertido.  
  
Na próxima e última lição, você criará uma simulação simples usando uma função personalizada do R e a executará no servidor remoto.  
  
## Próxima etapa  
[Lição 5: Criar uma simulação simples &#40;Aprofundamento da ciência de dados&#41;](../../advanced-analytics/r-services/lesson-5-create-a-simple-simulation-data-science-deep-dive.md)  
  
## Etapa anterior  
[Lição 4: Analisar dados no contexto de computação local &#40;Aprofundamento da ciência de dados&#41;](../../advanced-analytics/r-services/lesson-4-analyze-data-in-local-compute-context-data-science-deep-dive.md)  
  
## Consulte também  
[Aprofundamento da ciência de dados: Usando os pacotes RevoScaleR](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
