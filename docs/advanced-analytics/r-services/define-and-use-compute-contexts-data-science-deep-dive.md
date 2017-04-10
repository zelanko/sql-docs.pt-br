---
title: "Definir e usar contextos de computa&#231;&#227;o (Aprofundamento da ci&#234;ncia de dados) | Microsoft Docs"
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
ms.assetid: b13058d0-9c6a-44e1-849b-72189d9050ba
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Definir e usar contextos de computa&#231;&#227;o (Aprofundamento da ci&#234;ncia de dados)
Você decidiu que quer fazer alguns dos cálculos mais complexos no servidor, em vez de no computador local. Para fazer isso, você deve criar um contexto de computação que permite executar código do R no servidor.  
  
A função [RxInSqlServer](https://msdn.microsoft.com/microsoft-r/scaler/rxinsqlserver) é uma das funções avançadas do R aprimoradas fornecidas no pacote [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler). Ela trata as tarefas de criação da conexão de banco de dados e de transmissão de objetos entre o computador local e o contexto de execução remota.  
  
Nesta etapa, você aprenderá a usar a função *RxInSqlServer* para definir um contexto de computação em seu código R.  


  
## Criar e definir um contexto de computação  
Para criar um contexto de computação, são necessárias as seguintes informações básicas sobre a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   A cadeia de conexão da instância  
-   Uma especificação sobre como a saída deve ser tratada  
-   Argumentos opcionais para habilitar o rastreamento ou para especificar um diretório compartilhado


 Vamos começar.

1.  Especifique a cadeia de conexão da instância em que os cálculos ocorrerão.  Essa é apenas uma das diversas variáveis que você passará para a função *RxInSqlServer* para criar o contexto de computação. 

    **Usando um logon do SQL**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user name>;Pwd=<password>" 
      ```

    **Usando a autenticação integrada do Windows**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=DeepDive;Trusted_Connection=True"" 
      ```
2.  Especifique como deseja que a saída seja tratada. No código a seguir, você está indicando que a sessão do R na estação de trabalho deve sempre aguardar os resultados de trabalho do R, mas não retornar a saída do console das computações remotas.  
  
    ```R  
    sqlWait <- TRUE   
    sqlConsoleOutput <- FALSE   
    ```  
  
    O argumento *wait* para *RxInSqlServer* dá suporte a estas opções:  
  
    -   **TRUE**. O trabalho será bloqueado e não retornará até que seja concluído ou ocorra uma falha.  Para obter mais informações sobre trabalhos de bloqueio e não bloqueio, consulte 
  
    -   **FALSE**. Os trabalhos serão desbloqueados e retornarão imediatamente, permitindo que você continue a execução de outro código do R. No entanto, mesmo no modo desbloqueado, a conexão do cliente com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser mantida durante a execução do trabalho.  

3. Ou você pode especificar o local de um diretório local para uso compartilhado pela sessão do R local e pelo computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] remoto e suas contas.
    
    ```R  
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")   
    
    ## Add this line to create directory if it does not exist
    dir.create(sqlShareDir, recursive = TRUE) 
    ```  
    É recomendável que você use o padrão em vez de especificar manualmente uma pasta para esse argumento. Para obter mais informações, consulte [ScaleR reference (Referência do ScaleR)](https://msdn.microsoft.com/microsoft-r/scaler/rxinsqlserver).
    
    Se você apenas desejar saber qual pasta está sendo usada, você poderá executar o `rxGetComputeContext` para exibir detalhes sobre o atual contexto de computação. 
  

4.  Depois de preparar todas as variáveis, fornece-as como argumentos para o construtor `RxInSqlServer` para definir o objeto do contexto de computação.  
  
    ```R  
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,        
         #shareDir = sqlShareDir,       
         wait = sqlWait,   
         consoleOutput = sqlConsoleOutput)  
    ```  
  
    Você pode observar que a sintaxe para *RxInSqlServer* é quase idêntica à função *RxSqlServerData* usada anteriormente para definir a fonte de dados. No entanto, há algumas diferenças importantes.  
  
    -   O objeto da fonte de dados, definido usando a função *RxSqlServerData*, especifica o local em que os dados são armazenados.  
  
    -   Por outro lado, o contexto de computação (definido com a função *RxInSqlServer*) indica o local em que as agregações e outros cálculos deverão ocorrer.  
  
    A definição de um contexto de computação não afeta nenhuma outra computação R que você pode fazer na estação de trabalho e não altera a fonte dos dados. Por exemplo, você poderia definir um arquivo de texto local como a fonte de dados, mas alterar o contexto de computação para o SQL Server e executar todas as leituras e resumos nos dados no computador do SQL Server. 
  
## Habilitar o rastreamento no contexto de computação  
Às vezes, as operações que funcionam em seu contexto local enfrentam problemas quando estão em execução em um contexto de computação remota específica. se você desejar analisar problemas ou monitorar o desempenho, você poderá habilitar o rastreamento no contexto de computação para dar suporte à solução de problemas de tempo de execução.  
  
1. Crie um novo contexto de computação que use a mesma cadeia de conexão, mas adicione os argumentos *traceEnabled* e *traceLevel* ao construtor *RxInSqlServer*.  
  
    ```R  
    sqlComputeTrace <- RxInSqlServer(   
        connectionString = sqlConnString,        
        #shareDir = sqlShareDir,  
        wait = sqlWait,   
        consoleOutput = sqlConsoleOutput,       
        traceEnabled = TRUE,
        traceLevel = 7)  
    ```  
  
    Nesse exemplo, a propriedade *traceLevel* foi definida como 7, o que significa “mostrar todas as informações de rastreamento.”  

2. Para mudar para esse contexto de computação a qualquer momento, use a função *rxSetComputeContext* e especifique o contexto pelo nome.

    ```R  
    rxSetComputeContext( sqlComputeTrace)
    ```

    Para esse tutorial, nós usaremos o contexto de computação sem o rastreamento habilitado. O desempenho para a opção com rastreamento habilitado não foi testado para todas as operações e sua experiência pode variar dependendo da conectividade de rede.  
  
Agora que você criou um contexto de computação remota, você aprenderá a alterar os contextos de computação para executar o código R no servidor ou localmente.  
  
## Próxima etapa  
[Lição 2: Criar e executar scripts do R &#40;Aprofundamento da ciência de dados&#41;](../../advanced-analytics/r-services/lesson-2-create-and-run-r-scripts-data-science-deep-dive.md)  
  
## Etapa anterior  
[Consultar e modificar os dados do SQL Server &#40;Aprofundamento da ciência de dados&#41;](../../advanced-analytics/r-services/query-and-modify-the-sql-server-data-data-science-deep-dive.md)  
  
## Consulte também  
[Aprofundamento da ciência de dados: Usando os pacotes RevoScaleR](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
