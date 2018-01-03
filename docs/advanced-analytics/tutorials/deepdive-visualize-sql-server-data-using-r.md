---
title: " Visualizar dados do SQL Server usando o R (SQL e R mergulho profundo) | Microsoft Docs"
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs: R
ms.assetid: 10def0b3-9b09-4df9-b8aa-69516f7d7659
caps.latest.revision: "14"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 77321589a87230535502cc37a75bf09722abb66d
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2017
---
#  <a name="visualize-sql-server-data-using-r-sql-and-r-deep-dive"></a>Visualizar dados do SQL Server usando o R (SQL e R mergulho profundo)

Este artigo faz parte do tutorial mergulho profundo de ciência de dados, como usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Os pacotes avançados do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] incluem várias funções que foram otimizadas para escalabilidade e processamento paralelo. Normalmente, essas funções tem como prefixo **rx** ou **Rx**.

Para este passo a passo, você deve usar o **rxHistogram** função para exibir a distribuição de valores no _creditLine_ coluna sexo.

## <a name="visualize-data-using-rxhistogram"></a>Visualizar dados usando rxHistogram

1. Use o seguinte código R para chamar a função [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) e passar uma fórmula e fonte de dados. Você pode executá-lo localmente a princípio, para ver os resultados esperados e quanto tempo demora.
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    Internamente, **rxHistogram** chama a função [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) , que está incluída no pacote **RevoScaleR** . **rxCube** gera uma única lista (ou quadro de dados) que contém uma coluna para cada variável especificada na fórmula, além de uma coluna de contagens.
    
2. Agora, defina o contexto de computação para o computador remoto do SQL Server e execute **rxHistogram** novamente.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
 
3. Os resultados são exatamente os mesmos, uma vez que você está usando a mesma fonte de dados. No entanto, os cálculos são executados no computador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  Em seguida, os resultados são retornados à estação de trabalho local para plotagem.
   
![resultados do histograma](media/rsql-sue-histogramresults.jpg "resultados do histograma")

4. Você também pode chamar o **rxCube** de função e passar os resultados para um R plotagem de função.  Por exemplo, o exemplo a seguir usa **rxCube** para calcular a média de *fraudRisk* de cada combinação de *numTrans* e *numIntlTrans*:
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    Para especificar os grupos usados para calcular os meios de grupo, use a notação `F()` . Neste exemplo, `F(numTrans):F(numIntlTrans)` indica que os inteiros nas variáveis de `_numTrans` e `numIntlTrans` devem ser tratados como variáveis categóricas, com um nível para cada valor de inteiro.
  
    Como os níveis de baixos e altos já foram adicionados à fonte de dados `sqlFraudDS` (usando o `colInfo` parâmetro), os níveis são usados automaticamente no histograma.
  
5. O padrão retornam o valor de **rxCube** é um *rxCube objeto*, que representa uma referência cruzada. No entanto, você pode usar a função [rxResultsDF](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf) para converter os resultados em um quadro de dados que pode ser facilmente usado em uma das funções de plotagem do R padrão.
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    O **rxCube** função inclui um argumento opcional, *returnDataFrame* = **TRUE**, que você pode usar para converter os resultados em um quadro de dados diretamente. Por exemplo:
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    No entanto, a saída de **rxResultsDF** é muito mais limpa e preserva os nomes das colunas de origem.
  
6. Por fim, execute o seguinte código para criar um mapa de calor usando o `levelplot` de função do **entrelaçadas** pacote, que é incluído com todas as distribuições de R.
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **Resultados**
  
    ![resultados da dispersão](media/rsql-sue-scatterplotresults.jpg "resultados da dispersão")
  
Até mesmo com essa análise rápida, você pode ver que o risco de fraude aumenta com o número de transações e o número de transações internacionais.

Para obter mais informações sobre o **rxCube** função e referências cruzadas em geral, consulte [resumos de dados usando o RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries).

## <a name="next-step"></a>Próxima etapa

[Criar modelos de R usando dados do SQL Server](../../advanced-analytics/tutorials/deepdive-create-models.md)

## <a name="previous-step"></a>Etapa anterior

[Criar e executar scripts do R](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
