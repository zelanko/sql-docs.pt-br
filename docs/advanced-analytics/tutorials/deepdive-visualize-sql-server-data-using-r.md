---
title: Visualizar dados do SQL Server usando rxHistogram RevoScaleR - aprendizagem de máquina do SQL Server
description: Tutorial passo a passo sobre como visualizar dados usando a linguagem R no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 4f8ab37cefd55cd78556ac7bbf5af24cc01dca8e
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2018
ms.locfileid: "53596467"
---
#  <a name="visualize-sql-server-data-using-r-sql-server-and-revoscaler-tutorial"></a>Visualizar dados do SQL Server usando o R (tutorial do SQL Server e o RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Esta lição é parte do [tutorial de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar [funções RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Nesta lição, usar funções do R para exibir a distribuição de valores na *creditLine* coluna por gênero.

> [!div class="checklist"]
> * Criar variáveis de mínimo e máximo de entradas de histograma
> * Visualizar dados usando um histograma **rxHistogram** de **RevoScaleR**
> * Visualizar com gráficos de dispersão usando **levelplot** partir **Treliça** incluído na distribuição de R base

Conforme demonstrado nesta lição, você pode combinar funções específicas da Microsoft e de código-fonte aberto no mesmo script.

## <a name="add-maximum-and-minimum-values"></a>Adicionar valores mínimo e máximo

Com base em estatísticas de resumo calculadas na lição anterior, você descobriu algumas informações úteis sobre os dados que você pode inserir na fonte de dados para cálculos ainda mais. Por exemplo, os valores mínimo e máximo podem ser usados para calcular histogramas. Neste exercício, adicione os valores altos e baixos para o **RxSqlServerData** fonte de dados.

1. Comece configurando algumas variáveis temporárias.
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. Use a variável *ccColInfo* que você criou na lição anterior para definir as colunas na fonte de dados.
  
   Adicionar novas colunas computadas (*numTrans*, *numIntlTrans*, e *creditLine*) à coleção de colunas que substituir a definição original. O script a seguir adiciona fatores com base nos valores mínimos e máximo, obtidos do sumOut, que está armazenando a saída na memória do **rxSummary**. 
  
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
  
3. Tendo atualizado a coleção de colunas, aplique a instrução a seguir para criar uma versão atualizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fonte de dados que você definiu anteriormente.
  
    ```R
    sqlFraudDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlFraudTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
    A fonte de dados sqlFraudDS agora inclui as novas colunas adicionadas usando *ccColInfo*.
  
Neste ponto, as modificações afetam apenas o objeto de fonte de dados no R; Nenhum dado novo foi gravado na tabela de banco de dados ainda. No entanto, você pode usar os dados capturados na variável sumOut para criar visualizações e resumos. 

> [!TIP]
> Se você esquecer qual contexto de computação que você está usando, execute **rxGetComputeContext()**. Um valor de retorno de "Contexto de computação RxLocalSeq" indica que você está executando no contexto de computação local.

## <a name="visualize-data-using-rxhistogram"></a>Visualizar dados usando rxHistogram

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
 
3. Os resultados são exatamente iguais porque você está usando a mesma fonte de dados, mas na segunda etapa, os cálculos são executados no servidor remoto. Em seguida, os resultados são retornados à estação de trabalho local para plotagem.
   
  ![resultados do histograma](media/rsql-sue-histogramresults.jpg "resultados do histograma")


## <a name="visualize-with-scatter-plots"></a>Visualizar com gráficos de dispersão

Gráficos de dispersão são usados com frequência durante a exploração de dados para comparar a relação entre duas variáveis. Você pode usar pacotes de R internos para essa finalidade, com entradas fornecidas pelo **RevoScaleR** funções.

1. Chame o [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) função para calcular a média dos *fraudRisk* para cada combinação de *numTrans* e *numIntlTrans*:
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    Para especificar os grupos usados para calcular os meios de grupo, use a notação `F()` . Neste exemplo, `F(numTrans):F(numIntlTrans)` indica que os inteiros nas variáveis `numTrans` e `numIntlTrans` devem ser tratados como variáveis categóricas, com um nível para cada valor de inteiro.
  
    O padrão retornam o valor de **rxCube** é um *objeto rxCube*, que representa uma tabulação cruzada. 
  
2. Chame [rxResultsDF](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf) função para converter os resultados em um quadro de dados que pode ser facilmente usado em uma das funções de plotagem padrão do R.
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    O **rxCube** função inclui um argumento opcional, *returnDataFrame* = **TRUE**, que você pode usar para converter os resultados em um quadro de dados diretamente. Por exemplo:
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    No entanto, a saída de **rxResultsDF** é mais limpa e preserva os nomes das colunas de origem. Você pode executar `head(cube1)` seguido por `head(cubePlot)` para comparar a saída.
  
3. Criar um mapa de calor usando a **levelplot** função da **Treliça** package, incluído com todas as distribuições do R.
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **Resultados**
  
    ![resultados da dispersão](media/rsql-sue-scatterplotresults.jpg "resultados da dispersão")
  
Essa análise rápida, você pode ver que o risco de fraude aumenta com o número de transações e o número de transações internacionais.

Para obter mais informações sobre o **rxCube** função e tabelas de referência cruzada em geral, consulte [resumos de dados usando o RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries).

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Criar modelos de R usando dados do SQL Server](../../advanced-analytics/tutorials/deepdive-create-models.md)