---
title: "Definir e usar os contextos de computação (SQL e R mergulho profundo) | Microsoft Docs"
ms.custom: 
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs: R
ms.assetid: b13058d0-9c6a-44e1-849b-72189d9050ba
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 3db63204c3c2e904d2e4a8ba3fa8087bcfdbb1f5
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2017
---
# <a name="define-and-use-compute-contexts-sql-and-r-deep-dive"></a>Definir e usar os contextos de computação (SQL e R mergulho profundo)

Este artigo faz parte do tutorial mergulho profundo de ciência de dados, como usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Esta lição apresenta o [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) função, que permite que você definir um contexto de computação para o SQL Server e, em seguida, executar cálculos complexos no servidor, em vez de seu computador local. 

RevoScaleR suporta vários contextos de computação, de modo que você pode executar código R no Hadoop, Spark ou no banco de dados. Para o SQL Server, defina o servidor e a função controla as tarefas de criação de objetos de conexão e transmissão entre o computador local e o contexto de execução remota de banco de dados.

A função que cria o SQL Server de computação contexto usa as seguintes informações:

- Cadeia de caracteres de Conexão para a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância
- Especificação de como saída deve ser tratada
- Argumentos opcionais que habilitar o rastreamento ou especificam o nível de rastreamento
- Especificação opcional de um diretório de dados compartilhados

## <a name="create-and-set-a-compute-context"></a>Criar e definir um contexto de computação

1. Especifique a cadeia de conexão para a instância em que os cálculos são executados.  Novamente, você pode usar a cadeia de caracteres de conexão que você criou anteriormente. Se você deseja mover os cálculos em um servidor diferente ou use um logon diferente para executar algumas tarefas, você pode criar uma cadeia de caracteres de conexão diferente.

    **Usando um logon do SQL**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user name>;Pwd=<password>"
      ```

    **Usando a autenticação do Windows**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=DeepDive;Trusted_Connection=True"
      ```
2. Especifique como deseja que a saída seja tratada. No código a seguir, você está indicando que a sessão do R na estação de trabalho deve sempre aguardar os resultados de trabalho do R, mas não retornar a saída do console das computações remotas.
  
    ```R
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```
  
    O argumento *wait* para **RxInSqlServer** dá suporte a estas opções:
  
    -   **TRUE**. O trabalho está configurado como o bloqueio e não retorna até que ele foi concluído ou falhou.  Para obter mais informações, consulte [distribuída e a computação paralela no servidor de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing).
  
    -   **FALSE**. Trabalhos são configurados como sem bloqueio e retornam imediatamente, permitindo que você continue a execução de outro código de R. No entanto, mesmo no modo desbloqueado, a conexão do cliente com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser mantida durante a execução do trabalho.

3. Opcionalmente, você pode especificar o local de um diretório local para uso compartilhado, a sessão de R local e remoto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computador e suas contas.

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
4. Se você quiser criar manualmente um diretório específico para o compartilhamento, você pode adicionar uma linha semelhante ao seguinte:

    ```
    dir.create(sqlShareDir, recursive = TRUE)
    ```

    Para determinar a pasta que está sendo usada para o compartilhamento, execute `rxGetComputeContext()`, que retorna os detalhes sobre o atual contexto de computação. Para obter mais informações, consulte [ScaleR reference (Referência do ScaleR)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/).

4. Ter preparado todas as variáveis, fornecê-los como argumentos para o **RxInSqlServer** construtor para criar o *objeto de contexto de computação*.

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    A sintaxe para **RxInSqlServer** é quase idêntico do **RxSqlServerData** função usado anteriormente para definir a fonte de dados. No entanto, há algumas diferenças importantes.
      
    - O objeto da fonte de dados, definido usando a função [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata), especifica o local em que os dados são armazenados.
    
    - Por outro lado, o contexto de computação, definido por meio da função [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) indica onde as agregações e outros cálculos são ocorra.
    
    A definição de um contexto de computação não afeta nenhuma outra computação R que você pode fazer na estação de trabalho e não altera a fonte dos dados. Por exemplo, você poderia definir um arquivo de texto local como a fonte de dados, mas alterar o contexto de computação para o SQL Server e executar todas as leituras e resumos nos dados no computador do SQL Server.

## <a name="enable-tracing-on-the-compute-context"></a>Habilitar o rastreamento no contexto de computação

Às vezes, as operações funcionam em seu contexto local mas enfrentam problemas quando estão em execução em um contexto de computação remota. se você desejar analisar problemas ou monitorar o desempenho, você poderá habilitar o rastreamento no contexto de computação para dar suporte à solução de problemas de tempo de execução.

1. Criar um novo contexto de computação que usa a mesma cadeia de conexão, mas adicionar argumentos *traceEnabled* e *traceLevel* para o **RxInSqlServer** construtor.

    ```R
    sqlComputeTrace <- RxInSqlServer(
        connectionString = sqlConnString,
        #shareDir = sqlShareDir,
        wait = sqlWait,
        consoleOutput = sqlConsoleOutput,
        traceEnabled = TRUE,
        traceLevel = 7)
    ```
  
    Nesse exemplo, a propriedade *traceLevel* foi definida como 7, o que significa "mostrar todas as informações de rastreamento".

2. Para alterar o contexto de computação, use a função [rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) e especifique o contexto pelo nome.

    ```R
    rxSetComputeContext( sqlComputeTrace)
    ```

    > [!NOTE]
    > 
    > Para este tutorial, use o contexto de computação que não tenha habilitado o rastreamento. 
    > 
    > No entanto, se você decidir usar o rastreamento, lembre-se de que sua experiência pode ser afetada por conectividade de rede. Esteja ciente que porque não foi testado desempenho para a opção de rastreamento habilitado para todas as operações.

Na próxima etapa, que você aprenderá a usar compute contextos, para executar código R no servidor ou localmente.

## <a name="next-step"></a>Próxima etapa

[Criar e executar scripts do R](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)

## <a name="previous-step"></a>Etapa anterior

[Consultar e modificar os dados do SQL Server](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)
