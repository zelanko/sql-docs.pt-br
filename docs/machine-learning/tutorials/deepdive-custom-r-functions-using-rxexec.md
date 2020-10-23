---
title: Funções personalizadas do R usando a rxExec
description: Saiba como usar dados simulados para demonstrar a execução de uma função personalizada do R executada em um servidor remoto.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b8f03c64dc86e6d23113f3a35ae669f216b66489
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195148"
---
# <a name="run-custom-r-functions-on-sql-server-using-rxexec-sql-server-and-revoscaler-tutorial"></a>Executar funções personalizadas do R no SQL Server usando o rxExec (tutorial do SQL Server e do RevoScaleR)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Este é o tutorial 14 da [série de tutoriais do RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar as [funções do RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Neste tutorial, você usará dados simulados para demonstrar a execução de uma função personalizada do R executada em um servidor remoto.

Você pode executar funções do R personalizadas no contexto do SQL Server passando sua função por meio do [rxExec](/machine-learning-server/r-reference/revoscaler/rxexec), pressupondo que todas as bibliotecas exigidas pelo seu script também estejam instaladas no servidor e que essas bibliotecas sejam compatíveis com a distribuição base do R. 

A função **rxExec** no **RevoScaleR** fornece um mecanismo para executar qualquer script R que você precise. Além disso, a **rxExec** é capaz de distribuir explicitamente o trabalho entre vários núcleos em um único servidor, adicionando a escala aos scripts que, fora isso, são limitados às restrições de recursos do mecanismo nativo do R.

## <a name="prerequisites"></a>Pré-requisitos

+ [Serviços de Machine Learning do SQL Server (com o R)](../install/sql-machine-learning-services-windows-install.md) ou [SQL Server 2016 R Services (no banco de dados)](../install/sql-r-services-windows-install.md)
  
+ [Permissões de banco de dados](../security/user-permission.md) e logon do usuário do Banco de Dados do SQL Server

+ [Uma estação de trabalho de desenvolvimento com as bibliotecas RevoScaleR](../r/set-up-a-data-science-client.md)

A distribuição de R na estação de trabalho cliente fornece uma ferramenta interna **Rgui** que você pode usar para executar o script R neste tutorial. Você também pode usar um IDE como o RStudio ou as Ferramentas do R para Visual Studio.

## <a name="create-the-remote-compute-context"></a>Criar o contexto de computação remota

Execute os comandos do R a seguir em uma estação de trabalho cliente. Por exemplo, se você está usando o **Rgui**, inicie-o nesta localização: C:\Arquivos de Programas\Microsoft\R Client\R_SERVER\bin\x64\.

1. Especifique a cadeia de conexão da instância do SQL Server em que os cálculos serão realizados. O servidor deve ser configurado para integração com o R. O nome do banco de dados não é usado neste exercício, mas a cadeia de conexão requer que um seja fornecido. Se tiver um banco de dados de teste ou de exemplo, você poderá usá-lo.

    **Usando um logon do SQL**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>; Database=<database-name>;Uid=<SQL-user-name>;Pwd=<password>"
    ```

    **Usando a autenticação do Windows**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>;Database=<database-name>;Trusted_Connection=True"
    ```

2. Crie um contexto de computação remota para a instância do SQL Server referenciada na cadeia de conexão.

    ```R
    sqlCompute <- RxInSqlServer(connectionString = sqlConnString)
    ```

3. Ative o contexto de computação e, em seguida, retorne a definição do objeto como uma etapa de confirmação. Você deve ver as propriedades do objeto de contexto de computação.

    ```R
    rxSetComputeContext(sqlCompute)
    rxGetComputeContext()
    ```

## <a name="create-the-custom-function"></a>Criar a função personalizada

Neste exercício, você criará uma função personalizada do R que simulará um cassino comum, consistindo no lançamento de um par de dados. As regras do jogo determinam um resultado de vitória ou derrota:

+ Se obtiver 7 ou 11 no lançamento inicial, você ganhará.
+ Se obtiver 2, 3 ou 12, você perderá.
+ Se obtiver 4, 5, 6, 8, 9 ou 10, esse número se tornará seu ponto e você continuará lançando os dados até obter seu ponto novamente (nesse caso, você ganhará) ou até obter 7 (nesse caso, você perderá).

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
  
2.  Executando a função, simule um jogo de dados individual.
  
    ```R
    rollDice()
    ```
  
    Você ganhou ou perdeu?
  
Agora que você tem um script operacional, vamos ver como você pode executar a função **rxExec** várias vezes para criar uma simulação que ajuda a determinar a probabilidade de uma vitória.

## <a name="pass-rolldice-in-rxexec"></a>Passe rollDice() em rxExec

Para executar uma função arbitrária no contexto de um SQL Server remoto, chame a função **rxExec**.

1. Chame a função personalizada como um argumento para **rxExec**, juntamente com outros parâmetros que modificam a simulação.
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    + Use o argumento *timesToRun* para indicar quantas vezes a função deve ser executada.  Nesse caso, você lança os dados 20 vezes.
  
    + Os argumentos *RNGseed* e *RNGkind* podem ser usados para controlar a geração de números aleatórios. Quando *RNGseed* é definido como **automático**, um fluxo de número aleatório paralelo é inicializado em cada trabalhador.
  
2. A função **rxExec** cria uma lista com um elemento para cada execução; no entanto, você não verá um resultado real até que a lista seja concluída. Quando todas as iterações forem concluídas, a linha que começa com **length** retornará um valor.
  
    Em seguida, você pode ir para a próxima etapa para obter um resumo do registro de vitória/derrota.
  
3. Converta a lista retornada em um vetor usando a função **unlist** do R e resuma os resultados usando a função **table** .
  
    ```R
    table(unlist(sqlServerExec))
    ```
  
    Os resultados devem ser parecidos com este:
  
     *Derrota Vitória* *12 8*

## <a name="conclusion"></a>Conclusão

Embora este exercício seja simplista, ele demonstra um mecanismo importante para a integração de funções arbitrárias do R no script R em execução no SQL Server. Para resumir os principais pontos que tornam essa técnica possível:

+ O SQL Server deve ser configurado para aprendizado de máquina e integração ao R: [Serviços de Machine Learning do SQL Server](../install/sql-machine-learning-services-windows-install.md) com o recurso R ou [SQL Server 2016 R Services (no banco de dados)](../install/sql-r-services-windows-install.md).

+ As bibliotecas de software livre ou de terceiros usadas em sua função, incluindo quaisquer dependências, devem ser instaladas no SQL Server. Para obter mais informações, confira [Instalar novos pacotes do R](../package-management/install-additional-r-packages-on-sql-server.md).

+ Mover o script de um ambiente de desenvolvimento para um ambiente de produção protegido pode introduzir restrições de firewall e de rede. Teste cuidadosamente para verificar se o script é capaz de executar conforme o esperado.

## <a name="next-steps"></a>Próximas etapas

Para obter um exemplo mais complexo de como usar a **rxExec**, confira este artigo: [Paralelismo de granulação grosseira com foreach e rxExec](https://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)