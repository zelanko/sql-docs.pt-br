---
title: Definir e usar contextos de computação de RevoScaleR - aprendizagem de máquina do SQL Server
description: Tutorial passo a passo sobre como definir um contexto de computação usando a linguagem R no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3131dfc65d8964232073d37aba697f62de9fcc2a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962235"
---
# <a name="define-and-use-compute-contexts-sql-server-and-revoscaler-tutorial"></a>Definir e usar contextos de computação (tutorial do SQL Server e o RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Esta lição é parte do [tutorial de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar [funções RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Na lição anterior, você usou **RevoScaleR** funções para inspecionar objetos de dados. Esta lição apresenta a [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) função, que permite que você defina um contexto de computação para um SQL Server remoto. Com um contexto de computação remota, você pode alternar a execução de R de uma sessão local a uma sessão remota no servidor. 

> [!div class="checklist"]
> * Saiba o que contexto de computação de elementos de um SQL Server remoto
> * Habilitar o rastreamento em um objeto de contexto de computação

**RevoScaleR** dá suporte a vários contextos de computação: Hadoop, Spark no HDFS e SQL Server no banco de dados. Para o SQL Server, o **RxInSqlServer** função é usada para conexões de servidor e objetos de transmissão entre o computador local e o contexto de execução remota.

## <a name="create-and-set-a-compute-context"></a>Criar e definir um contexto de computação

O **RxInSqlServer** função que cria o contexto de computação do SQL Server usa as seguintes informações:

+ Cadeia de caracteres de Conexão para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância
+ Especificação de como a saída deve ser tratada
+ Especificação opcional de um diretório de dados compartilhados
+ Argumentos opcionais que habilitar o rastreamento ou especificar o nível de rastreamento

Esta seção orienta você por meio de cada parte.

1. Especifique a cadeia de conexão para a instância em que os cálculos são executados. Novamente, você pode usar a cadeia de caracteres de conexão que você criou anteriormente.

    **Usando um logon do SQL**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user nme>;Pwd=<password>"
      ```

    **Usando a autenticação do Windows**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=RevoDeepDive;Trusted_Connection=True"
    ```
    
2. Especifique como deseja que a saída seja tratada. O script a seguir instrui a sessão local do R para aguardar os resultados do trabalho de R no servidor antes de processar a próxima operação. Ele também suprime a saída das computações remotas apareça na sessão local.
  
    ```R
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```
  
    O argumento *wait* para **RxInSqlServer** dá suporte a estas opções:
  
    -   **TRUE**. O trabalho está configurado como o bloqueio e não retorna até que ele tenha sido concluída ou falhou.  Para obter mais informações, consulte [distribuído e computação paralela no Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing).
  
    -   **FALSE**. Trabalhos são configurados como desbloqueados e retornarão imediatamente, permitindo que você continue a execução de outro código de R. No entanto, mesmo no modo desbloqueado, a conexão do cliente com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser mantida durante a execução do trabalho.

3. Opcionalmente, especifique o local de um diretório local para uso compartilhado por sessão do R local e remoto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computador e suas contas.

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
   Se você quiser criar manualmente um diretório específico para o compartilhamento, você pode adicionar uma linha semelhante à seguinte:

    ```R
    dir.create(sqlShareDir, recursive = TRUE)
    ```

4. Passar argumentos para o **RxInSqlServer** construtor para criar a *objeto de contexto de computação*.

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

5. Ative o contexto de computação remota.

    ```R
    rxSetComputeContext(sqlCompute)
    ```

6. Retornam informações sobre o contexto de computação, incluindo suas propriedades.

    ```R
    rxGetComputeContext()
    ```

7. Redefina o contexto de computação de volta para o computador local, especificando a palavra-chave "local" (a próxima lição demonstra como usar o contexto de computação remota).

    ```R
    rxSetComputeContext("local")
    ```

> [!Tip]
> Para obter uma lista de outras palavras-chave com suporte nesta função, digite `help("rxSetComputeContext")` em uma linha de comando do R.

## <a name="enable-tracing"></a>Habilitar o rastreamento

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

2. Use o [rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) função para especificar o contexto de computação de rastreamento habilitado por nome.

    ```R
    rxSetComputeContext(sqlComputeTrace)
    ```

## <a name="next-steps"></a>Próximas etapas

Saiba como alternar contextos de computação para executar código R no servidor ou localmente.

> [!div class="nextstepaction"]
> [Contextos de computação de estatísticas de resumo de computação no local e remoto](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)