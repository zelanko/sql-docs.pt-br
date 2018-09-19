---
title: Definir e usar contextos de computação (SQL e R aprofundamento) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6a76e07cb2ecd03a59112f6c39e3fa2f7895e0a2
ms.sourcegitcommit: aa9d2826e3c451f4699c0e69c9fcc8a2781c6213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/17/2018
ms.locfileid: "45975635"
---
# <a name="define-and-use-compute-contexts-sql-and-r-deep-dive"></a>Definir e usar contextos de computação (SQL e R aprofundamento)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo faz parte do tutorial de aprofundamento de ciência de dados, sobre como usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Esta lição apresenta a [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) função, que permite definir um contexto de computação para o SQL Server e, em seguida, executar cálculos complexos no servidor, em vez de seu computador local. 

RevoScaleR dá suporte a vários contextos de computação, para que você pode executar código R no Hadoop, Spark ou no banco de dados. Para o SQL Server, defina o servidor e a função manipula as tarefas de criação de objetos de conexão e passando entre o computador local e o contexto de execução remota de banco de dados.

A função que cria o SQL Server de computação contexto usa as seguintes informações:

- Cadeia de caracteres de Conexão para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância
- Especificação de como a saída deve ser tratada
- Argumentos opcionais que habilitar o rastreamento ou especificar o nível de rastreamento
- Especificação opcional de um diretório de dados compartilhados

## <a name="create-and-set-a-compute-context"></a>Criar e definir um contexto de computação

1. Especifique a cadeia de conexão para a instância em que os cálculos são executados.  Novamente, você pode usar a cadeia de caracteres de conexão que você criou anteriormente. Se você quiser mover os cálculos para um servidor diferente ou use um logon diferente para executar algumas tarefas, você pode criar uma cadeia de caracteres de conexão diferente.

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
  
    -   **TRUE**. O trabalho está configurado como o bloqueio e não retorna até que ele tenha sido concluída ou falhou.  Para obter mais informações, consulte [distribuído e computação paralela no Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing).
  
    -   **FALSE**. Trabalhos são configurados como desbloqueados e retornarão imediatamente, permitindo que você continue a execução de outro código de R. No entanto, mesmo no modo desbloqueado, a conexão do cliente com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser mantida durante a execução do trabalho.

3. Opcionalmente, você pode especificar o local de um diretório local para uso compartilhado por sessão do R local e remoto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computador e suas contas.

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
4. Se você quiser criar manualmente um diretório específico para o compartilhamento, você pode adicionar uma linha semelhante à seguinte:

    ```
    dir.create(sqlShareDir, recursive = TRUE)
    ```

    Para determinar qual pasta está sendo usada atualmente para o compartilhamento, execute `rxGetComputeContext()`, que retorna detalhes sobre o atual contexto de computação. Para obter mais informações, consulte [ScaleR reference (Referência do ScaleR)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/).

4. Depois de preparar todas as variáveis, fornece-as como argumentos para o **RxInSqlServer** construtor para criar a *objeto de contexto de computação*.

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    A sintaxe **RxInSqlServer** parece ser praticamente idêntico do **RxSqlServerData** função que você usou anteriormente para definir a fonte de dados. No entanto, há algumas diferenças importantes.
      
    - O objeto da fonte de dados, definido usando a função [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata), especifica o local em que os dados são armazenados.
    
    - Em contraste, o contexto de computação, definido por meio da função [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) indica onde as agregações e outros cálculos deverão ocorrer.
    
    A definição de um contexto de computação não afeta nenhuma outra computação R que você pode fazer na estação de trabalho e não altera a fonte dos dados. Por exemplo, você poderia definir um arquivo de texto local como a fonte de dados, mas alterar o contexto de computação para o SQL Server e executar todas as leituras e resumos nos dados no computador do SQL Server.

## <a name="enable-tracing-on-the-compute-context"></a>Habilitar o rastreamento no contexto de computação

Às vezes, as operações funcionam em seu contexto local mas enfrentam problemas quando estão em execução em um contexto de computação remota. Se você quiser analisar problemas ou monitorar o desempenho, você pode habilitar o rastreamento no contexto de computação, para dar suporte à solução de problemas de tempo de execução.

1. Criar um novo contexto de computação que usa a mesma cadeia de conexão, mas adicione os argumentos *traceEnabled* e *traceLevel* para o **RxInSqlServer** construtor.

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
    > Para este tutorial, use o contexto de computação que não tenha o rastreamento habilitado. 
    > 
    > No entanto, se você decidir usar o rastreamento, lembre-se de que sua experiência pode ser afetada por conectividade de rede. Além disso, lembre que porque o desempenho para a opção de rastreamento habilitado não foi testado para todas as operações.

Na próxima etapa, que você aprenderá a usar contextos de computação do, executar código R no servidor ou localmente.

## <a name="next-step"></a>Próxima etapa

[Criar e executar scripts do R](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)

## <a name="previous-step"></a>Etapa anterior

[Consultar e modificar os dados do SQL Server](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)
