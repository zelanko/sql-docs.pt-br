---
title: "Definir e usar contextos de computação (Aprofundamento da ciência de dados) | Microsoft Docs"
ms.custom: 
ms.date: 05/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: b13058d0-9c6a-44e1-849b-72189d9050ba
caps.latest.revision: 17
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 511738cfce795600bcfa06a95de4cdf3d6b503bb
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="define-and-use-compute-contexts"></a>Definir e usar contextos de computação


Suponha que você quer fazer alguns dos cálculos mais complexos no servidor, em vez de no computador local. Para fazer isso, você pode criar um contexto de computação, que permite que o código R seja executado no servidor.

A função **RxInSqlServer** é uma das funções avançadas do R aprimoradas fornecidas no pacote [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler) . Ela trata as tarefas de criação da conexão de banco de dados e de transmissão de objetos entre o computador local e o contexto de execução remota.

Nesta etapa, você aprenderá a usar a função **RxInSqlServer** para definir um contexto de computação em seu código R.

Para criar um contexto de computação, são necessárias as seguintes informações básicas sobre a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :

- A cadeia de conexão da instância
- Uma especificação sobre como a saída deve ser tratada
- Argumentos opcionais para habilitar o rastreamento ou para especificar um diretório compartilhado

## <a name="create-and-set-a-compute-context"></a>Criar e definir um contexto de computação

1. Especifique a cadeia de conexão da instância em que os cálculos ocorrerão.  Essa é apenas uma das diversas variáveis que você passará para a função *RxInSqlServer* para criar o contexto de computação. Você pode usar novamente a cadeia de conexão que você criou anteriormente ou você pode criar uma cadeia diferente, caso deseje mover os cálculos para um servidor diferente ou usar uma identidade diferente.

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
  
    O argumento *wait* para *RxInSqlServer* dá suporte a estas opções:
  
    -   **TRUE**. O trabalho será bloqueado e não retornará até que seja concluído ou ocorra uma falha.  Para obter mais informações, consulte [distribuída e a computação paralela em R Microsoft](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing).
  
    -   **FALSE**. Os trabalhos serão desbloqueados e retornarão imediatamente, permitindo que você continue a execução de outro código do R. No entanto, mesmo no modo desbloqueado, a conexão do cliente com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser mantida durante a execução do trabalho.

3. Ou você pode especificar o local de um diretório local para uso compartilhado pela sessão do R local e pelo computador do  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] remoto e suas contas.

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
4. Se você quiser criar manualmente um diretório específico para o compartilhamento, você pode adicionar uma linha semelhante ao seguinte. Para determinar a pasta que está sendo usada para o compartilhamento, execute `rxGetComputeContext`, que retorna os detalhes sobre o atual contexto de computação. Para obter mais informações, consulte [ScaleR reference (Referência do ScaleR)](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxinsqlserver).

    ```
    dir.create(sqlShareDir, recursive = TRUE)
    ```

4. Ter preparado todas as variáveis, fornecê-los como argumentos para o construtor RxInSqlServer para criar o *objeto de contexto de computação*.

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    Você pode observar que a sintaxe para RxInSqlServer * é praticamente idêntica da função RxSqlServerData que você usou anteriormente para definir a fonte de dados. No entanto, há algumas diferenças importantes.
      
    - O objeto de fonte de dados, definido por meio da função RxSqlServerData, especifica onde os dados são armazenados.
    
    - Em contraste, o contexto de computação (definido por meio da função RxInSqlServer) indica onde as agregações e outros cálculos são ocorra.
    
    A definição de um contexto de computação não afeta nenhuma outra computação R que você pode fazer na estação de trabalho e não altera a fonte dos dados. Por exemplo, você poderia definir um arquivo de texto local como a fonte de dados, mas alterar o contexto de computação para o SQL Server e executar todas as leituras e resumos nos dados no computador do SQL Server.

## <a name="enable-tracing-on-the-compute-context"></a>Habilitar o rastreamento no contexto de computação

Às vezes, as operações funcionam em seu contexto local mas enfrentam problemas quando estão em execução em um contexto de computação remota. se você desejar analisar problemas ou monitorar o desempenho, você poderá habilitar o rastreamento no contexto de computação para dar suporte à solução de problemas de tempo de execução.

1. Criar um novo contexto de computação que usa a mesma cadeia de conexão, mas adicionar argumentos *traceEnabled* e *traceLevel* para o *RxInSqlServer* construtor.

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

2. Para alterar o contexto de computação, use a função rxSetComputeContext e especifique o contexto por nome.

    ```R
    rxSetComputeContext( sqlComputeTrace)
    ```

    > [!NOTE]
    > 
    > Para esse tutorial, nós usaremos o contexto de computação sem o rastreamento habilitado. Isso ocorre porque o desempenho para a opção de rastreamento habilitado não foi testado para todas as operações.
    > 
    > No entanto, se você decidir usar o rastreamento, lembre-se de que sua experiência pode ser afetada por conectividade de rede.

Agora que você criou um contexto de computação remota, você aprenderá a alterar os contextos de computação para executar o código R no servidor ou localmente.

## <a name="next-step"></a>Próxima etapa

[Criar e executar Scripts de R](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)


## <a name="previous-step"></a>Etapa anterior

[Consultar e modificar os dados do SQL Server](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)



