---
title: "Li&#231;&#227;o 5: Criar uma simula&#231;&#227;o simples (Aprofundamento da ci&#234;ncia de dados) | Microsoft Docs"
ms.custom: ""
ms.date: "10/03/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: f420b816-ddab-4a1a-89b9-c8285a2d33a3
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# Li&#231;&#227;o 5: Criar uma simula&#231;&#227;o simples (Aprofundamento da ci&#234;ncia de dados)
Até agora você estava usando as funções do R fornecidas pelo SQL Server R Services projetadas especificamente para mover dados entre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e um contexto de computação local. No entanto, suponha que você escreva uma função personalizada do R e deseje executá-la no contexto do servidor?  
  
Você pode chamar uma função arbitrária no contexto do computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], usando a função *rxExec*. Você também pode usar o *rxExec* para distribuir o trabalho explicitamente entre os núcleos em um único nó de servidor.  
  
Nesta lição, você aprenderá a usar o servidor remoto para criar uma simulação simples. A simulação não exige dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; o exemplo demonstra apenas como criar uma função personalizada e chamá-la usando a função *rxExec*.  
  
Para obter um exemplo mais complexo de como usar *rxExec*, consulte este artigo: [http://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html](http://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)  
  
## Criar a função  
Um jogo de casino comum consiste em jogar um par de dados, com estas regras:  
  
-   Se você obtiver 7 ou 11 no lançamento inicial, você ganhará.  
  
-   Se você obtiver 2, 3 ou 12, você perderá.  
  
-   Se você obtiver 4, 5, 6, 8, 9 ou 10, esse número se tornará seu ponto e você continuará lançando os dados até obter seu ponto novamente (nesse caso, você ganhará); se obtiver 7, você perderá.  
  
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
  
2.  Para simular um jogo de dados simples, execute a função.  
  
    ```R  
    rollDice()   
    ```  
  
    Você ganhou ou perdeu?  
  
Agora vamos ver como você pode executar a função várias vezes, para criar uma simulação que ajuda a determinar a probabilidade de uma vitória.  
  
## Criar a simulação  
Para executar uma função arbitrária no contexto do computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], chame a função *rxExec*. Embora a *rxExec* também dê suporte à execução distribuída de uma função em paralelo em vários nós ou núcleos em um contexto de servidor, aqui você o usará para executar sua função personalizada no servidor.  
  
1.  Chame a função personalizada como um argumento para *rxExec*, juntamente com outros parâmetros que modificam a simulação.  
  
    ```R  
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")   
    length(sqlServerExec)   
    ```  
  
    -   Use o argumento *timesToRun* para indicar quantas vezes a função deve ser executada.  Nesse caso, você lança os dados 20 vezes.  
  
    -   Os argumentos *RNGseed* e *RNGkind* podem ser usados para controlar a geração de números aleatórios. Quando *RNGseed* é definido como **automático**, um fluxo de número aleatório paralelo é inicializado em cada trabalhador.  
  
2.  A função *rxExec* cria uma lista com um elemento para cada execução; no entanto, você não verá um resultado real até que a lista seja concluída. Quando todas as iterações forem concluídas, a linha que começa com `length` retornará um valor.  
  
    Em seguida, você pode ir para a próxima etapa para obter um resumo do registro de vitória/derrota.  
  
3.  Converta a lista retornada em um vetor usando a função *unlist* do R e resuma os resultados usando a função *table*.  
  
    ```R  
    table(unlist(sqlServerExec))  
    ```  
  
    Os resultados devem ser parecidos com este:  
  
     *Derrota Vitória*   
     *12  8*  
  
## Conclusões  
Neste tutorial, você se tornou proficiente nestas tarefas:  
  
-   Obter dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para usá-los em análises  
  
-   Criar e modificar fontes de dados no R  
  
-   Passar modelos, dados e plotagens entre a estação de trabalho e o servidor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
>  [!TIP]
> 
> Caso você queira experimentar essas técnicas usando um conjunto de dados maior com 10 milhões de observações, os arquivos de dados estão disponíveis em [http://packages.revolutionanalytics.com/datasets](http://packages.revolutionanalytics.com/datasets).  
>   
> Para usar novamente este passo a passo com os arquivos de dados maiores, basta baixar os dados e modificar as fontes de dados da seguinte maneira:   
>  -   Definir as variáveis *ccFraudCsv* e *ccScoreCsv* para apontar para os novos arquivos de dados     
>  -   Alterar o nome da tabela referenciada em *sqlFraudTable* para *ccFraud10*    
>  -   Alterar o nome da tabela referenciada em *sqlScoreTable* para *ccFraudScore10*   
  
## Etapa anterior  
[Mover dados entre o SQL Server e o arquivo XDF &#40;Aprofundamento da ciência de dados&#41;](../../advanced-analytics/r-services/move-data-between-sql-server-and-xdf-file-data-science-deep-dive.md)  
  
  
  
