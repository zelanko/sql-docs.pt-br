---
title: Criar uma simulação simple (SQL e R mergulho profundo) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7c93d91324233b05541c09e037f5043f2d9e376f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31202878"
---
# <a name="create-a-simple-simulation-sql-and-r-deep-dive"></a>Criar uma simulação simple (SQL e R mergulho profundo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo é a última etapa no tutorial mergulho profundo de ciência de dados, como usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Até agora você estava usando funções de R são projetadas especificamente para mover dados entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e contexto de computação local. No entanto, suponha que você escreva uma função personalizada do R e deseje executá-la no contexto do servidor?

Você pode chamar uma função arbitrária no contexto do computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , usando a função [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) . Você também pode usar **rxExec** explicitamente distribuem o trabalho entre núcleos em um único servidor.

Nesta lição, você pode usar o servidor remoto para criar um simples de simulação. A simulação não exige dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ; o exemplo demonstra apenas como criar uma função personalizada e chamá-la usando a função **rxExec** .

Para obter um exemplo mais complexo do uso de **rxExec**, consulte este artigo: [paralelismo grãos grandes com foreach e rxExec](http://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)

## <a name="create-the-custom-function"></a>Criar a função personalizada

Um jogo de casino comum consiste em jogar um par de dados, com estas regras:

- Se você obtiver 7 ou 11 no lançamento inicial, você ganhará.
- Se você obtiver 2, 3 ou 12, você perderá.
- Se você obtiver 4, 5, 6, 8, 9 ou 10, esse número se tornará seu ponto e você continuará lançando os dados até obter seu ponto novamente (nesse caso, você ganhará); se obtiver 7, você perderá.

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
                { result \<- "Loss" }
                else if (count > 1 && roll == 7 )
                { result \<- "Loss" }
                else if (count > 1 && point == roll)
                { result <- "Win" }
                else { count <- count + 1 }
            }
            result
    }
    ```
  
2.  Para simular um jogo único de dados, execute a função.
  
    ```R
    rollDice()
    ```
  
    Você ganhou ou perdeu?
  
Agora vamos ver como você pode usar **rxExec** para executar a função várias vezes, para criar uma simulação que ajuda a determinar a probabilidade de uma boa ideia.

## <a name="create-the-simulation"></a>Criar a simulação

Para executar uma função arbitrária no contexto do computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , chame a função **rxExec** . Embora **rxExec** também dá suporte à execução distribuída de uma função em paralelo em nós ou núcleos em um contexto de servidor, aqui ele executa a função personalizados no computador do SQL Server.

1. Chame a função personalizada como um argumento para **rxExec**, junto com outros parâmetros que modificam a simulação.
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    - Use o argumento *timesToRun* para indicar quantas vezes a função deve ser executada.  Nesse caso, você lança os dados 20 vezes.
  
    - Os argumentos *RNGseed* e *RNGkind* podem ser usados para controlar a geração de números aleatórios. Quando *RNGseed* é definido como **automático**, um fluxo de número aleatório paralelo é inicializado em cada trabalhador.
  
2. A função **rxExec** cria uma lista com um elemento para cada execução; no entanto, você não verá um resultado real até que a lista seja concluída. Quando todas as iterações forem concluídas, a linha que começa com `length` retornará um valor.
  
    Em seguida, você pode ir para a próxima etapa para obter um resumo do registro de vitória/derrota.
  
3. Converta a lista retornada em um vetor usando a função `unlist` do R e resuma os resultados usando a função `table` .
  
    ```R
    table(unlist(sqlServerExec))
    ```
  
    Os resultados devem ser parecidos com este:
  
     *Perda Win* *12 8*

## <a name="conclusions"></a>Conclusões

Neste tutorial, você se tornou proficiente nestas tarefas:
  
-   Obter dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para usá-los em análises
  
-   Criar e modificar fontes de dados no R
  
-   Passar modelos, dados e plotagens entre a estação de trabalho e o servidor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
  

Se você quiser fazer experiências com essas técnicas usando um conjunto de dados maior de 10 milhões de observações, os arquivos de dados estão disponíveis no site da Revolution analytics: [índice de conjuntos de dados](http://packages.revolutionanalytics.com/datasets)

Para usar novamente este passo a passo com os arquivos de dados maior, baixa os dados e, em seguida, modificar cada uma das fontes de dados da seguinte maneira:

1. Modificar as variáveis `ccFraudCsv` e `ccScoreCsv` para apontar para os novos arquivos de dados
2. Alterar o nome da tabela referenciada em *sqlFraudTable* para `ccFraud10`
3. Alterar o nome da tabela referenciada em *sqlScoreTable* para `ccFraudScore10`

## <a name="additional-samples"></a>Exemplos adicionais

Agora que você conheça o uso de funções de RevoScaler para passar e transformar dados e contextos de computação, consulte estes tutoriais:

[Tutoriais de R para serviços de aprendizado de máquina](machine-learning-services-tutorials.md)
## <a name="previous-step"></a>Etapa anterior

[Mover dados entre o SQL Server e o arquivo XDF](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)
