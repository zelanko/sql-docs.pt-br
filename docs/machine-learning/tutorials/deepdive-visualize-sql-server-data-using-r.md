---
title: Visualizar dados usando o RevoScaleR
description: 'Tutorial 6 do RevoScaleR: Como visualizar dados usando a linguagem R no SQL Server.'
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4cc97db70461797e2e37614ae33d23ed51b21147
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116719"
---
#  <a name="visualize-sql-server-data-using-r-sql-server-and-revoscaler-tutorial"></a>Visualizar dados do SQL Server usando o R (tutorial de SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este é o tutorial 6 da [série de tutoriais do RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar as [funções do RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Neste tutorial, você usará as funções do R para exibir a distribuição de valores na coluna *creditLine* por gênero.

> [!div class="checklist"]
> * Criar variáveis mín-máx para entradas de histograma
> * Visualizar dados em um histograma usando **rxHistogram** do **RevoScaleR**
> * Visualizar com gráficos de dispersão usando **levelplot** do pacote **malha** incluído na distribuição de R base

Conforme demonstrado nesse tutorial, você pode combinar funções de software livre e específicas da Microsoft no mesmo script.

## <a name="add-maximum-and-minimum-values"></a>Adicionar valores máximos e mínimos

Com base nas estatísticas de resumo calculadas no tutorial anterior, você descobriu algumas informações úteis sobre os dados que pode inserir na fonte de dados para cálculos adicionais. Por exemplo, os valores mínimo e máximo podem ser usados para computar histogramas. Neste exercício, adicione os valores alto e baixo à fonte de dados **RxSqlServerData**.

1. Comece configurando algumas variáveis temporárias.
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. Use a variável *ccColInfo* que você criou no tutorial anterior para definir as colunas na fonte de dados.
  
   Adicione novas colunas calculadas (*numTrans*, *numIntlTrans*e *creditLine*) à coleção de colunas que substituem a definição original. O script a seguir adiciona fatores com base nos valores mínimo e máximo obtidos de sumOut, que está armazenando a saída na memória de **rxSummary**. 
  
    ```R 
    ccColInfo <- list(
        gender = list(type = "factor",
          levels = c("1", "2"), 
          newLevels = c("Male", "Female")),
        cardholder = list(type = "factor",
          levels = c("1", "2"), 
          newLevels = c("Principal", "Secondary")), 
        state = list(type = "factor", 
          levels = as.character(1:51), 
          newLevels = stateAbb), 
        balance  = list(type = "numeric"),
        numTrans = list(type = "factor", 
          levels = as.character(sumDF[var == "numTrans", "Min"]:sumDF[var == "numTrans", "Max"])),
        numIntlTrans = list(type = "factor",  
            levels = as.character(sumDF[var == "numIntlTrans", "Min"]:sumDF[var =="numIntlTrans", "Max"])),
        creditLine = list(type = "numeric")
            )
    ```
  
3. Após atualizar a coleção de colunas, aplique a instrução a seguir para criar uma versão atualizada da fonte de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você definiu anteriormente.
  
    ```R
    sqlFraudDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlFraudTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
    A fonte de dados sqlFraudDS agora inclui as novas colunas adicionadas usando *ccColInfo*.
  
Neste ponto, as modificações afetam apenas o objeto de fonte de dados em R. Nenhum dado novo foi gravado na tabela de banco de dados ainda. No entanto, você pode usar os dados capturados na variável sumOut para criar visualizações e resumos. 

> [!TIP]
> Se você esquecer qual contexto de computação está usando, execute **rxGetComputeContext()** . Um valor retornado de "Contexto de Computação de RxLocalSeq" indica que você está executando no contexto de computação local.

## <a name="visualize-data-using-rxhistogram"></a>Visualizar dados usando o rxHistogram

1. Use o seguinte código R para chamar a função [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) e passar uma fórmula e fonte de dados. Você pode executá-lo localmente a princípio, para ver os resultados esperados e quanto tempo demora.
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    Internamente, **rxHistogram** chama a função [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) , que está incluída no pacote **RevoScaleR** . **rxCube** gera uma única lista (ou quadro de dados) que contém uma coluna para cada variável especificada na fórmula, além de uma coluna de contagens.
    
2. Agora, defina o contexto de computação para o computador remoto do SQL Server e execute **rxHistogram** novamente.
  
    ```R
    rxSetComputeContext(sqlCompute)
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
3. Os resultados são exatamente os mesmos porque você está usando a mesma fonte de dados, mas na segunda etapa, os cálculos são executados no servidor remoto. Em seguida, os resultados são retornados à estação de trabalho local para plotagem.
   
  ![resultados do histograma](media/rsql-sue-histogramresults.jpg "resultados do histograma")


## <a name="visualize-with-scatter-plots"></a>Visualizar com gráficos de dispersão

Os gráficos de dispersão são frequentemente usados durante a exploração de dados para comparar a relação entre duas variáveis. Você pode usar pacotes R internos para essa finalidade, com entradas fornecidas por funções de **RevoScaleR**.

1. Chame a função [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) para calcular a média de *fraudRisk* para cada combinação de *numTrans* e *numIntlTrans*:
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    Para especificar os grupos usados para calcular os meios de grupo, use a notação `F()` . Neste exemplo, `F(numTrans):F(numIntlTrans)` indica que os inteiros nas variáveis `numTrans` e `numIntlTrans` devem ser tratados como variáveis categóricas, com um nível para cada valor inteiro.
  
    O valor retornado padrão de **rxCube** é um *objeto rxCube*, que representa uma tabulação cruzada. 
  
2. Chame a função [rxResultsDF](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf) para converter os resultados em um quadro de dados que pode ser facilmente usado em uma das funções de plotagem do R padrão.
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    A função **rxCube** inclui um argumento opcional, *returnDataFrame* = **TRUE**, que você poderá usar para converter os resultados em um quadro de dados diretamente. Por exemplo:
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    No entanto, a saída de **rxResultsDF** é mais limpa e preserva os nomes das colunas de origem. Você pode executar `head(cube1)` seguido por `head(cubePlot)` para comparar a saída.
  
3. Crie um mapa de calor usando a função **levelplot** do pacote **malha** incluído em todas as distribuições do R.
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **Resultados**
  
    ![resultados do gráfico de dispersão](media/rsql-sue-scatterplotresults.jpg "resultados do gráfico de dispersão")
  
Com essa análise rápida, você pode ver que o risco de fraude aumenta com o número de transações e o número de transações internacionais.

Para saber mais sobre a função **rxCube** e tabelas cruzadas em geral, confira [Resumos de dados com RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries).

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Criar modelos de R usando dados do SQL Server](../../machine-learning/tutorials/deepdive-create-models.md)