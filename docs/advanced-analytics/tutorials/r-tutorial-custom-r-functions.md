---
title: Executar funções de R personalizadas no SQL Server usando o RevoScaleR rxExec - aprendizagem de máquina do SQL Server
description: Tutorial passo a passo sobre como executar script R personalizado no SQL Server usando as funções RevoScaleR.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 90790c2b96843ea1821b8b4ed05052a7611cdf74
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2018
ms.locfileid: "53596437"
---
# <a name="run-custom-r-functions-on-sql-server-using-rxexec"></a>Executar funções de R personalizadas no SQL Server usando rxExec
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Você pode executar funções de R personalizadas no contexto do SQL Server, passando a sua função por meio [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec), supondo que todas as bibliotecas requer que seu script também são instaladas no servidor e essas bibliotecas são compatíveis com a base distribuição de R. 

O **rxExec** funcionar **RevoScaleR** fornece um mecanismo para executar qualquer script de R que você precisa. Além disso, **rxExec** é capaz de distribuir o trabalho explicitamente entre os vários núcleos em um único servidor, adicionando a escala para scripts que limitam-se caso contrário, as restrições de recursos do mecanismo de R nativo.

Neste tutorial, você usará dados simulados para demonstrar a execução de uma função personalizada do R que é executado em um servidor remoto.

## <a name="prerequisites"></a>Prerequisites

+ [Serviços de aprendizado de máquina do SQL Server 2017 (com R)](../install/sql-machine-learning-services-windows-install.md) ou [SQL Server 2016 R Services (no banco de dados)](../install/sql-r-services-windows-install.md)
  
+ [Permissões de banco de dados](../security/user-permission.md) e um logon de usuário de banco de dados do SQL Server

+ [Uma estação de trabalho de desenvolvimento com as bibliotecas de RevoScaleR](../r/set-up-a-data-science-client.md)

A distribuição de R na estação de trabalho cliente fornece uma interna **Rgui** ferramenta que você pode usar para executar o script de R neste tutorial. Você também pode usar um IDE, como RStudio ou as ferramentas do R para Visual Studio.

## <a name="create-the-remote-compute-context"></a>Criar o contexto de computação remota

Execute os seguintes comandos de R em uma estação de trabalho do cliente. Por exemplo, você estiver usando **Rgui**, iniciá-lo a partir deste local: C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64\.

1. Especifique a cadeia de conexão para a instância do SQL Server em que os cálculos são executados. O servidor deve ser configurado para integração do R. O nome do banco de dados não é usado neste exercício, mas a cadeia de caracteres de conexão requer um. Se você tiver um banco de dados de teste ou de exemplo, você pode usá-lo.

    **Usando um logon do SQL**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>; Database=<database-name>;Uid=<SQL-user-name>;Pwd=<password>"
    ```

    **Usando a autenticação do Windows**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>;Database=<database-name>;Trusted_Connection=True"
    ```

2. Crie um contexto de computação remota para a instância do SQL Server referenciado na cadeia de conexão.

    ```R
    sqlCompute <- RxInSqlServer(connectionString = sqlConnString)
    ```

3. Ative o contexto de computação e, em seguida, retornar a definição de objeto como uma etapa de confirmação. Você deve ver as propriedades do objeto de contexto de computação.

    ```R
    rxSetComputeContext(sqlCompute)
    rxGetComputeContext()
    ```

## <a name="create-the-custom-function"></a>Crie a função personalizada

Neste exercício, você criará uma função personalizada do R que simula um casino comum consiste em jogar um par de dice. Regras do jogo determinam um resultado de perda ou win:

+ Obtiver 7 ou 11 no lançamento inicial, você ganha.
+ Reverter 2, 3 ou 12, você perderá.
+ Reverter um 4, 5, 6, 8, 9 ou 10, esse número se tornará seu ponto e você continuará lançando os dados até que você obter seu ponto novamente (nesse caso, você ganhará) ou reverte um 7, nesse caso, você perderá.

O jogo é facilmente simulado no R, com a criação de uma função personalizada e sua execução repetida.

1.  Crie a função personalizada usando o código R a seguir:
  
    ```R
    rollDice <- function()
    {
        result <- NULL
        point <- NULL
        count <- 1
            while (is.null(result))
            {
                roll <- sum(sample(6, 2, replace=TRUE))
  
                if (is.null(point))
                { point <- roll }
                if (count == 1 && (roll == 7 || roll == 11))
                {  result <- "Win" }
                else if (count == 1 && (roll == 2 || roll == 3 || roll == 12))
                { result <- "Loss" }
                else if (count > 1 && roll == 7 )
                { result <- "Loss" }
                else if (count > 1 && point == roll)
                { result <- "Win" }
                else { count <- count + 1 }
            }
            result
    }
    ```
  
2.  Simule um jogo de dados simples, executando a função.
  
    ```R
    rollDice()
    ```
  
    Você ganhou ou perdeu?
  
Agora que você tem um script operacional, vamos ver como você pode usar **rxExec** para executar a função várias vezes para criar uma simulação que ajuda a determinar a probabilidade de uma vitória.

## <a name="pass-rolldice-in-rxexec"></a>Passe rollDice() rxExec

Para executar uma função arbitrária no contexto de um SQL Server remoto, chame o **rxExec** função.

1. Chame a função personalizada como um argumento para **rxExec**, juntamente com outros parâmetros que modificam a simulação.
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    + Use o argumento *timesToRun* para indicar quantas vezes a função deve ser executada.  Nesse caso, você lança os dados 20 vezes.
  
    + Os argumentos *RNGseed* e *RNGkind* podem ser usados para controlar a geração de números aleatórios. Quando *RNGseed* é definido como **automático**, um fluxo de número aleatório paralelo é inicializado em cada trabalhador.
  
2. A função **rxExec** cria uma lista com um elemento para cada execução; no entanto, você não verá um resultado real até que a lista seja concluída. Quando todas as iterações forem concluídas, a linha que começa com **comprimento** retornará um valor.
  
    Em seguida, você pode ir para a próxima etapa para obter um resumo do registro de vitória/derrota.
  
3. Converta a lista retornada em um vetor usando a função **unlist** do R e resuma os resultados usando a função **table** .
  
    ```R
    table(unlist(sqlServerExec))
    ```
  
    Os resultados devem ser parecidos com este:
  
     *Derrota vitória* *12 8*

## <a name="conclusion"></a>Conclusão

Embora este exercício é simplista, ele demonstra um mecanismo importante para a integração de funções do R arbitrárias no script de R em execução no SQL Server. Para resumir os principais pontos que possibilitam essa técnica:

+ SQL Server deve ser configurado para integração de R e aprendizado de máquina: [Serviços de aprendizado de máquina do SQL Server 2017](../install/sql-machine-learning-services-windows-install.md) com o recurso de R, ou [SQL Server 2016 R Services (no banco de dados)](../install/sql-r-services-windows-install.md).

+ Bibliotecas de terceiros ou de código-fonte aberto usadas em sua função, incluindo as dependências, devem ser instaladas no SQL Server. Para obter mais informações, consulte [instalar novos pacotes de R](../r/install-additional-r-packages-on-sql-server.md).

+ Mover o script de um ambiente de desenvolvimento para um ambiente de produção protegido pode introduzir restrições de firewall e rede. Teste cuidadosamente para garantir que o script é capaz de executar conforme o esperado.

## <a name="next-steps"></a>Próximas etapas

Para obter um exemplo mais complexo do uso **rxExec**, consulte este artigo: [Paralelismo de grãos grandes com foreach e rxExec](https://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)
