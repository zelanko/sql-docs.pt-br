---
title: Executar funções de R personalizadas em SQL Server usando RevoScaleR rxExec
description: Tutorial explicativo sobre como executar o script R personalizado no SQL Server usando as funções RevoScaleR.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 439b21bce4e081025db1db53ab44498415ca44af
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715411"
---
# <a name="run-custom-r-functions-on-sql-server-using-rxexec"></a>Executar funções de R personalizadas em SQL Server usando rxExec
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Você pode executar funções de R personalizadas no contexto de SQL Server passando sua função via [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec), supondo que todas as bibliotecas que o seu script requer também estejam instaladas no servidor e essas bibliotecas sejam compatíveis com a distribuição base do R. 

A função **rxExec** no **RevoScaleR** fornece um mecanismo para executar qualquer script R que você precisar. Além disso, o **rxExec** é capaz de distribuir explicitamente o trabalho entre vários núcleos em um único servidor, adicionando escala a scripts que, de outra forma, são limitados às restrições de recursos do mecanismo do R nativo.

Neste tutorial, você usará dados simulados para demonstrar a execução de uma função personalizada do R que é executada em um servidor remoto.

## <a name="prerequisites"></a>Pré-requisitos

+ [SQL Server serviços de Machine Learning (com R)](../install/sql-machine-learning-services-windows-install.md) ou [SQL Server 2016 R Services (no banco de dados)](../install/sql-r-services-windows-install.md)
  
+ [Permissões de banco de dados](../security/user-permission.md) e um logon de usuário de banco de dados SQL Server

+ [Uma estação de trabalho de desenvolvimento com as bibliotecas RevoScaleR](../r/set-up-a-data-science-client.md)

A distribuição de R na estação de trabalho cliente fornece uma ferramenta interna de **Rgui** que você pode usar para executar o script R neste tutorial. Você também pode usar um IDE como RStudio ou Ferramentas do R para Visual Studio.

## <a name="create-the-remote-compute-context"></a>Criar o contexto de computação remota

Execute os comandos do R a seguir em uma estação de trabalho cliente. Por exemplo, você está usando **Rgui**, inicie-o neste local: C:\Arquivos de Files\Microsoft\R Client\R_SERVER\bin\x64\.

1. Especifique a cadeia de conexão para a instância de SQL Server em que as computações são executadas. O servidor deve ser configurado para a integração do R. O nome do banco de dados não é usado neste exercício, mas a cadeia de conexão requer um. Se você tiver um banco de dados de teste ou de exemplo, poderá usá-lo.

    **Usando um logon do SQL**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>; Database=<database-name>;Uid=<SQL-user-name>;Pwd=<password>"
    ```

    **Usando a autenticação do Windows**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>;Database=<database-name>;Trusted_Connection=True"
    ```

2. Crie um contexto de computação remota para a instância de SQL Server referenciada na cadeia de conexão.

    ```R
    sqlCompute <- RxInSqlServer(connectionString = sqlConnString)
    ```

3. Ative o contexto de computação e, em seguida, retorne a definição de objeto como uma etapa de confirmação. Você deve ver as propriedades do objeto de contexto de computação.

    ```R
    rxSetComputeContext(sqlCompute)
    rxGetComputeContext()
    ```

## <a name="create-the-custom-function"></a>Criar a função personalizada

Neste exercício, você criará uma função personalizada do R que simula um casino comum que consiste em reverter um par de data. As regras do jogo determinam um resultado de ganho ou perda:

+ Lance um 7 ou 11 no seu lançamento inicial, você ganha.
+ Roll 2, 3 ou 12, você perde.
+ Lance um 4, 5, 6, 8, 9 ou 10, esse número se tornará seu ponto e você continuará a ser revertido até que você lance seu ponto novamente (nesse caso, você ganha) ou lance um 7, caso em que você perderá.

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
  
2.  Simule um único jogo de negócios executando a função.
  
    ```R
    rollDice()
    ```
  
    Você ganhou ou perdeu?
  
Agora que você tem um script operacional, vamos ver como você pode usar **rxExec** para executar a função várias vezes para criar uma simulação que ajuda a determinar a probabilidade de um ganho.

## <a name="pass-rolldice-in-rxexec"></a>Passe rollDice () em rxExec

Para executar uma função arbitrária no contexto de um SQL Server remoto, chame a função **rxExec** .

1. Chame a função personalizada como um argumento para **rxExec**, junto com outros parâmetros que modificam a simulação.
  
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
  
     *Ganho de perda* *12 8*

## <a name="conclusion"></a>Conclusão

Embora este exercício seja simplista, ele demonstra um mecanismo importante para a integração de funções R arbitrárias no script R em execução no SQL Server. Para resumir os principais pontos que tornam essa técnica possível:

+ SQL Server deve ser configurado para aprendizado de máquina e integração de R: [SQL Server serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md) com o recurso R ou [SQL Server 2016 R Services (no banco de dados)](../install/sql-r-services-windows-install.md).

+ As bibliotecas de software livre ou de terceiros usadas em sua função, incluindo quaisquer dependências, devem ser instaladas em SQL Server. Para obter mais informações, consulte [instalar novos pacotes de R](../r/install-additional-r-packages-on-sql-server.md).

+ Mover o script de um ambiente de desenvolvimento para um ambientes de produção protegidos pode introduzir restrições de firewall e rede. Teste cuidadosamente para verificar se o script é capaz de executar conforme o esperado.

## <a name="next-steps"></a>Próximas etapas

Para obter um exemplo mais complexo de como usar o **rxExec**, consulte este artigo: [Paralelismo de granulação grosseira com foreach e rxExec](https://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)
