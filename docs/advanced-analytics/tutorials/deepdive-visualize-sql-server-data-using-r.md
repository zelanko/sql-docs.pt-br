---
title: Visualizar dados de SQL Server usando RevoScaleR rxHistogram
description: Tutorial explicativo sobre como Visualizar dados usando a linguagem R em SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8c7e837f9ed4392a8ecfc9e7c237b95f3fdde3d3
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714857"
---
#  <a name="visualize-sql-server-data-using-r-sql-server-and-revoscaler-tutorial"></a>Visualizar dados de SQL Server usando o R (tutorial de SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Esta lição faz parte do [tutorial do RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar as [funções do RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com SQL Server.

Nesta lição, use as funções do R para exibir a distribuição de valores na coluna de *crédito* por gênero.

> [!div class="checklist"]
> * Criar variáveis Min-Max para entradas de histograma
> * Visualizar dados em um histograma usando **rxHistogram** do **RevoScaleR**
> * Visualizar com gráficos de dispersão usando o **levelplot** do **malha** incluído na distribuição de R base

Como esta lição demonstra, você pode combinar funções de código-fonte aberto e específicas da Microsoft no mesmo script.

## <a name="add-maximum-and-minimum-values"></a>Adicionar valores máximo e mínimo

Com base nas estatísticas de resumo computadas da lição anterior, você descobriu algumas informações úteis sobre os dados que você pode inserir na fonte de dados para cálculos adicionais. Por exemplo, os valores mínimo e máximo podem ser usados para computar histogramas. Neste exercício, adicione os valores alto e baixo à fonte de dados **RxSqlServerData** .

1. Comece configurando algumas variáveis temporárias.
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. Use a variável *ccColInfo* que você criou na lição anterior para definir as colunas na fonte de dados.
  
   Adicione novas colunas computadas (*numTrans*, *numIntlTrans*e *credite*) à coleção de colunas que substituem a definição original. O script a seguir adiciona fatores com base em valores mínimos e máximos obtidos em sumOut, que está armazenando a saída na memória de **rxSummary**. 
  
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
  
3. Após atualizar a coleção de colunas, aplique a instrução a seguir para criar uma versão atualizada [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da fonte de dados que você definiu anteriormente.
  
    ```R
    sqlFraudDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlFraudTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
    A fonte de dados sqlFraudDS agora inclui as novas colunas adicionadas usando *ccColInfo*.
  
Neste ponto, as modificações afetam apenas o objeto de fonte de dados em R; nenhum dado novo foi gravado na tabela de banco de dados ainda. No entanto, você pode usar os dados capturados na variável sumOut para criar visualizações e resumos. 

> [!TIP]
> Se você se esquecer do contexto de computação que está usando, execute **rxGetComputeContext ()** . Um valor de retorno de "contexto de computação RxLocalSeq" indica que você está executando no contexto de computação local.

## <a name="visualize-data-using-rxhistogram"></a>Visualizar dados usando o rxHistogram

1. Use o seguinte código R para chamar a função [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) e passar uma fórmula e fonte de dados. Você pode executá-lo localmente a princípio, para ver os resultados esperados e quanto tempo demora.
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    Internamente, **rxHistogram** chama a função [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) , que está incluída no pacote **RevoScaleR** . **rxCube** gera uma única lista (ou quadro de dados) que contém uma coluna para cada variável especificada na fórmula, além de uma coluna de contagens.
    
2. Agora, defina o contexto de computação para o computador SQL Server remoto e execute **rxHistogram** novamente.
  
    ```R
    rxSetComputeContext(sqlCompute)
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
3. Os resultados são exatamente os mesmos porque você está usando a mesma fonte de dados, mas na segunda etapa, os cálculos são executados no servidor remoto. Em seguida, os resultados são retornados à estação de trabalho local para plotagem.
   
  ![resultados do histograma](media/rsql-sue-histogramresults.jpg "resultados do histograma")


## <a name="visualize-with-scatter-plots"></a>Visualizar com gráficos de dispersão

As plotagens de dispersão são frequentemente usadas durante a exploração de dados para comparar a relação entre duas variáveis. Você pode usar pacotes R internos para essa finalidade, com entradas fornecidas pelas funções **RevoScaleR** .

1. Chame a função [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) para calcular a média de *fraudRisk* para cada combinação de *numTrans* e *numIntlTrans*:
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    Para especificar os grupos usados para calcular os meios de grupo, use a notação `F()` . Neste exemplo, `F(numTrans):F(numIntlTrans)` indica que os inteiros nas variáveis `numTrans` e `numIntlTrans` devem ser tratados como variáveis categóricas, com um nível para cada valor inteiro.
  
    O valor de retorno padrão de **rxCube** é um *objeto rxCube*, que representa uma tabulação cruzada. 
  
2. Chame a função [rxResultsDF](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf) para converter os resultados em um quadro de dados que pode ser facilmente usado em uma das funções de plotagem padrão de R.
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    A função **rxCube** inclui um argumento opcional, *returnDataFrame* = **true**, que você pode usar para converter os resultados em um quadro de dados diretamente. Por exemplo:
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    No entanto, a saída de **rxResultsDF** é limpa e preserva os nomes das colunas de origem. Você pode executar `head(cube1)` seguido pelo `head(cubePlot)` para comparar a saída.
  
3. Crie um mapa de calor usando a função **levelplot** do pacote **malha** , incluído com todas as distribuições de R.
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **Resultados**
  
    ![resultados da dispersão](media/rsql-sue-scatterplotresults.jpg "resultados da dispersão")
  
Nessa análise rápida, você pode ver que o risco de fraude aumenta com o número de transações e o número de transações internacionais.

Para obter mais informações sobre a função **rxCube** e tabelas em geral, consulte resumos de [dados usando o RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries).

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Criar modelos de R usando dados de SQL Server](../../advanced-analytics/tutorials/deepdive-create-models.md)