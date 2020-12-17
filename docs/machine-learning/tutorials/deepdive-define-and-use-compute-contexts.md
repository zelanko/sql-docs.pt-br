---
title: Usar contextos de computação do RevoScaleR
description: Saiba mais sobre a função RxInSqlServer, que permite definir um contexto de computação para um SQL Server remoto.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: 074597a032fbcaa8231dfea22d567204cb079f58
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470547"
---
# <a name="define-and-use-compute-contexts-sql-server-and-revoscaler-tutorial"></a>Definir e usar contextos de computação (tutorial do SQL Server e do RevoScaleR)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Este é o tutorial 4 da [série de tutoriais do RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar as [funções do RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

No tutorial anterior, você usou as funções do **RevoScaleR** para inspecionar objetos de dados. Este tutorial apresenta a função [RxInSqlServer](/machine-learning-server/r-reference/revoscaler/rxinsqlserver), que permite definir um contexto de computação para um SQL Server remoto. Com um contexto de computação remota, você pode alternar a execução de R de uma sessão local para uma sessão remota no servidor. 

> [!div class="checklist"]
> * Conhecer os elementos de um contexto de computação do SQL Server remoto
> * Habilitar o rastreamento em um objeto de contexto de computação

O **RevoScaleR** dá suporte a vários contextos de computação: Hadoop, Spark no HDFS e SQL Server no banco de dados. Para o SQL Server, a função **RxInSqlServer** é usada para conexões de servidor e passar objetos entre o computador local e o contexto de execução remota.

## <a name="create-and-set-a-compute-context"></a>Criar e definir um contexto de computação

A função **RxInSqlServer** que cria o contexto de computação do SQL Server usa as seguintes informações:

+ Cadeia de conexão da instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
+ Especificação de como a saída deve ser tratada
+ Especificação opcional de um diretório de dados compartilhados
+ Argumentos opcionais que habilitam o rastreamento ou especificam o nível de rastreamento

Esta seção orienta você em cada parte.

1. Especifique a cadeia de conexão da instância em que os cálculos serão realizados. Você pode usar novamente a cadeia de conexão que criou anteriormente.

    **Usando um logon do SQL**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user nme>;Pwd=<password>"
      ```

    **Usando a autenticação do Windows**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=RevoDeepDive;Trusted_Connection=True"
    ```
    
2. Especifique como deseja que a saída seja tratada. O script a seguir direciona a sessão local do R para aguardar os resultados do trabalho do R no servidor antes de processar a próxima operação. Ele também impede que a saída de cálculos remotos apareça na sessão local.
  
    ```R
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```
  
    O argumento *wait* para **RxInSqlServer** dá suporte a estas opções:
  
    -   **TRUE**. O trabalho é configurado como bloqueio e não é retornado até que tenha sido concluído ou ocorra uma falha.  Para obter mais informações, confira [Computação distribuída e paralela no Machine Learning Server](/machine-learning-server/r/how-to-revoscaler-distributed-computing).
  
    -   **FALSE**. Os trabalhos são configurados como sem bloqueio e são retornados imediatamente, permitindo que você continue a execução de outro código do R. No entanto, mesmo no modo desbloqueado, a conexão do cliente com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser mantida durante a execução do trabalho.

3. Ou especifique a localização de um diretório local para uso compartilhado pela sessão do R local e pelo computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] remoto e suas contas.

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
   Se desejar criar manualmente um diretório específico para compartilhamento, você poderá adicionar uma linha como a seguinte:

    ```R
    dir.create(sqlShareDir, recursive = TRUE)
    ```

4. Passe argumentos para o construtor **RxInSqlServer** para definir o *objeto do contexto de computação*.

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    A sintaxe para **RxInSqlServer** é quase idêntica à da função **RxSqlServerData** usada anteriormente para definir a fonte de dados. No entanto, há algumas diferenças importantes.
      
    - O objeto da fonte de dados, definido usando a função [RxSqlServerData](/machine-learning-server/r-reference/revoscaler/rxsqlserverdata), especifica o local em que os dados são armazenados.
    
    - Por outro lado, o contexto de computação, definido com a função [RxInSqlServer](/machine-learning-server/r-reference/revoscaler/rxinsqlserver), indica o local em que as agregações e outros cálculos deverão ocorrer.
    
    A definição de um contexto de computação não afeta nenhuma outra computação R que você pode fazer na estação de trabalho e não altera a fonte dos dados. Por exemplo, você poderia definir um arquivo de texto local como a fonte de dados, mas alterar o contexto de computação para o SQL Server e executar todas as leituras e resumos nos dados no computador do SQL Server.

5. Ative o contexto de computação remota.

    ```R
    rxSetComputeContext(sqlCompute)
    ```

6. Retorne informações sobre o contexto de computação, incluindo suas propriedades.

    ```R
    rxGetComputeContext()
    ```

7. Redefina o contexto de computação como o computador local especificando a palavra-chave "local" (o próximo tutorial demonstra o uso do contexto de computação remota).

    ```R
    rxSetComputeContext("local")
    ```

> [!Tip]
> Para obter uma lista de outras palavras-chave com suporte nesta função, digite `help("rxSetComputeContext")` em uma linha de comando do R.

## <a name="enable-tracing"></a>Habilitar o rastreamento

Às vezes, as operações funcionam em seu contexto local mas enfrentam problemas quando estão em execução em um contexto de computação remota. Se você desejar analisar problemas ou monitorar o desempenho, poderá habilitar o rastreamento no contexto de computação para dar suporte à solução de problemas de tempo de execução.

1. Crie um contexto de computação que use a mesma cadeia de conexão, mas adicione os argumentos *traceEnabled* e *traceLevel* ao construtor **RxInSqlServer**.

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

2. Use a função [rxSetComputeContext](/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) para especificar o contexto de computação habilitado para rastreamento por nome.

    ```R
    rxSetComputeContext(sqlComputeTrace)
    ```

## <a name="next-steps"></a>Próximas etapas

Saiba como alternar contextos de computação para executar o código R no servidor ou localmente.

> [!div class="nextstepaction"]
> [Calcular estatísticas de resumo em contextos de computação local e remota](../../machine-learning/tutorials/deepdive-create-and-run-r-scripts.md)