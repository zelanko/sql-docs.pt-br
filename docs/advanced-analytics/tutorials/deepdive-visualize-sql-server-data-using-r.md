---
title: "Visualizar dados do SQL Server usando o R (Aprofundamento da ciência de dados) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/18/2017
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
ms.assetid: 10def0b3-9b09-4df9-b8aa-69516f7d7659
caps.latest.revision: 14
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 023958a137515c519fe8d73e1ce1181dc7579356
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="visualize-sql-server-data-using-r"></a>Visualizar dados do SQL Server usando o R

Os pacotes avançados do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] incluem várias funções que foram otimizadas para escalabilidade e processamento paralelo. Normalmente, essas funções tem como prefixo *rx* ou *Rx*.

Para este passo a passo, você usará a função **rxHistogram** para exibir a distribuição dos valores na coluna _creditLine_ por gênero.

## <a name="visualize-data-using-rxhistogram"></a>Visualizar dados usando rxHistogram

1. Use o seguinte código R para chamar a função rxHistogram e passar uma fórmula e fonte de dados. Você pode executá-lo localmente a princípio, para ver os resultados esperados e quanto tempo demora.
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    Internamente, rxHistogram chama a função rxCube, que está incluída no **RevoScaleR** pacote. A função rxCube gera uma única lista (ou quadro de dados) que contém uma coluna para cada variável especificada na fórmula, além de uma coluna de contagens.
    
2. Agora, defina o contexto de computação para o computador remoto do SQL Server e execute rxHistogram novamente.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
 
3. Os resultados são exatamente os mesmos, uma vez que você está usando a mesma fonte de dados. No entanto, os cálculos são executados no computador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  Em seguida, os resultados são retornados à estação de trabalho local para plotagem.
   
![resultados do histograma](media/rsql-sue-histogramresults.jpg "resultados do histograma")

4. Você também pode chamar a função rxCube e passar os resultados para uma função de plotagem de R.  Por exemplo, o exemplo a seguir usa rxCube para calcular a média de *fraudRisk* para cada combinação de *numTrans* e *numIntlTrans*:
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    Para especificar os grupos usados para calcular os meios de grupo, use a notação `F()` . Neste exemplo, `F(numTrans):F(numIntlTrans)` indica que os inteiros nas variáveis _numTrans_ e _numIntlTrans_ devem ser tratados como variáveis categóricas, com um nível para cada valor de inteiro.
  
    Como os níveis baixo e alto já foram adicionados à fonte de dados *sqlFraudDS* (usando o parâmetro *colInfo* ), os níveis serão usados no histograma automaticamente.
  
5. O valor de retorno de rxCube é por padrão uma *rxCube objeto*, que representa uma referência cruzada. No entanto, você pode usar a função **rxResultsDF** para converter os resultados em um quadro de dados que pode ser facilmente usado em uma das funções de plotagem do R padrão.
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    > [!TIP]
    > 
    > Observe que a função rxCube inclui um argumento opcional, *returnDataFrame* = TRUE, que você pode usar para converter os resultados em um quadro de dados diretamente. Por exemplo:
    >   
    > `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
    >   
    > No entanto, a saída de rxResultsDF é mais limpa e preserva os nomes das colunas de origem.
  
6. Por fim, execute o seguinte código para criar um mapa de calor usando o `levelplot` de função do **entrelaçadas** pacote, que é incluído com todas as distribuições de R.
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **Resultados**
  
    ![resultados da dispersão](media/rsql-sue-scatterplotresults.jpg "resultados da dispersão")
  
Até mesmo com essa análise rápida, você pode ver que o risco de fraude aumenta com o número de transações e o número de transações internacionais.

Para obter mais informações sobre a função de rxCube e referências cruzadas em geral, consulte [resumos de dados](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-summaries).

## <a name="next-step"></a>Próxima etapa

[Criar modelos](../../advanced-analytics/tutorials/deepdive-create-models.md)

## <a name="previous-step"></a>Etapa anterior

[Lição 2: Criar e executar scripts do R](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)



