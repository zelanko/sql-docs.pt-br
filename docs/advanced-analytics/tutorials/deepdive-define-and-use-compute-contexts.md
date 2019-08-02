---
title: Definir e usar contextos de computação RevoScaleR
description: Tutorial explicativo sobre como definir um contexto de computação usando a linguagem R no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c5fb28af293c549a9f5494ab08c6c01ebf5d2a20
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715540"
---
# <a name="define-and-use-compute-contexts-sql-server-and-revoscaler-tutorial"></a>Definir e usar contextos de computação (tutorial de SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Esta lição faz parte do [tutorial do RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar as [funções do RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com SQL Server.

Na lição anterior, você usou as funções **RevoScaleR** para inspecionar objetos de dados. Esta lição apresenta a função [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) , que permite definir um contexto de computação para um SQL Server remoto. Com um contexto de computação remota, você pode alternar a execução de R de uma sessão local para uma sessão remota no servidor. 

> [!div class="checklist"]
> * Aprenda os elementos de um contexto de computação de SQL Server remota
> * Habilitar o rastreamento em um objeto de contexto de computação

O **RevoScaleR** dá suporte a vários contextos de computação: Hadoop, Spark no HDFS e SQL Server no banco de dados. Por SQL Server, a função **RxInSqlServer** é usada para conexões de servidor e passagem de objetos entre o computador local e o contexto de execução remota.

## <a name="create-and-set-a-compute-context"></a>Criar e definir um contexto de computação

A função **RxInSqlServer** que cria o contexto de computação SQL Server usa as seguintes informações:

+ Cadeia de conexão para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a instância
+ Especificação de como a saída deve ser tratada
+ Especificação opcional de um diretório de dados compartilhados
+ Argumentos opcionais que habilitam o rastreamento ou especificam o nível de rastreamento

Esta seção orienta você em cada parte.

1. Especifique a cadeia de conexão para a instância em que as computações são executadas. Você pode usar novamente a cadeia de conexão que você criou anteriormente.

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
  
    -   **TRUE**. O trabalho é configurado como bloqueio e não retorna até que seja concluído ou tenha falhado.  Para obter mais informações, consulte [computação paralela e distribuída no Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing).
  
    -   **FALSE**. Os trabalhos são configurados como sem bloqueio e retornam imediatamente, permitindo que você continue executando outro código do R. No entanto, mesmo no modo desbloqueado, a conexão do cliente com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser mantida durante a execução do trabalho.

3. Opcionalmente, especifique o local de um diretório local para uso compartilhado pela sessão do R local e pelo computador remoto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e suas contas.

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
   Se você quiser criar manualmente um diretório específico para compartilhamento, poderá adicionar uma linha semelhante à seguinte:

    ```R
    dir.create(sqlShareDir, recursive = TRUE)
    ```

4. Passe os argumentos para o construtor **RxInSqlServer** para criar o *objeto de contexto de computação*.

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    A sintaxe de **RxInSqlServer** parece quase idêntica à da função **RxSqlServerData** que você usou anteriormente para definir a fonte de dados. No entanto, há algumas diferenças importantes.
      
    - O objeto da fonte de dados, definido usando a função [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata), especifica o local em que os dados são armazenados.
    
    - Por outro lado, o contexto de computação, definido usando a função [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) , indica onde as agregações e outros cálculos devem ocorrer.
    
    A definição de um contexto de computação não afeta nenhuma outra computação R que você pode fazer na estação de trabalho e não altera a fonte dos dados. Por exemplo, você poderia definir um arquivo de texto local como a fonte de dados, mas alterar o contexto de computação para o SQL Server e executar todas as leituras e resumos nos dados no computador do SQL Server.

5. Ative o contexto de computação remota.

    ```R
    rxSetComputeContext(sqlCompute)
    ```

6. Retornar informações sobre o contexto de computação, incluindo suas propriedades.

    ```R
    rxGetComputeContext()
    ```

7. Redefina o contexto de computação de volta para o computador local especificando a palavra-chave "local" (a próxima lição demonstra como usar o contexto de computação remota).

    ```R
    rxSetComputeContext("local")
    ```

> [!Tip]
> Para obter uma lista de outras palavras-chave com suporte nesta função, digite `help("rxSetComputeContext")` em uma linha de comando do R.

## <a name="enable-tracing"></a>Habilitar o rastreamento

Às vezes, as operações funcionam em seu contexto local mas enfrentam problemas quando estão em execução em um contexto de computação remota. Se você quiser analisar problemas ou monitorar o desempenho, poderá habilitar o rastreamento no contexto de computação para dar suporte à solução de problemas em tempo de execução.

1. Crie um novo contexto de computação que usa a mesma cadeia de conexão, mas adicione os argumentos *traceEnabled* e *TraceLevel* ao construtor **RxInSqlServer** .

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

2. Use a função [rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) para especificar o contexto de computação habilitado para rastreamento por nome.

    ```R
    rxSetComputeContext(sqlComputeTrace)
    ```

## <a name="next-steps"></a>Próximas etapas

Saiba como alternar contextos de computação para executar o código R no servidor ou localmente.

> [!div class="nextstepaction"]
> [Calcular estatísticas de resumo em contextos de computação local e remota](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)