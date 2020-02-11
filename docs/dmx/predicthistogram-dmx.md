---
title: PredictHistogram (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fdc63d1c93d1290c701233cb94f71f157c771182
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68893857"
---
# <a name="predicthistogram-dmx"></a>PredictHistogram (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna uma tabela que representa um histograma para a previsão de uma determinada coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
PredictHistogram(<scalar column reference> | <cluster column reference>)  
```  
  
## <a name="applies-to"></a>Aplica-se A  
 Uma referência de coluna escalar ou uma referência de coluna de cluster. Pode ser usado com todos os tipos de algoritmo, exceto o algoritmo de Associação do [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
## <a name="return-type"></a>Tipo de retorno  
 Uma tabela.  
  
## <a name="remarks"></a>Comentários  
 Um histograma gera colunas de estatísticas. A estrutura de coluna do histograma retornado depende do tipo de referência de coluna usada com a função **PredictHistogram** .  
  
## <a name="scalar-columns"></a>Colunas escalares  
 Para uma \<referência de coluna escalar>, o histograma que a função **PredictHistogram** retorna consiste nas seguintes colunas:  
  
-   Valor sendo previsto.  
  
-   **$Support**  
  
-   **$Probability**  
  
-   **$ProbabilityVariance**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)]os algoritmos de Data Mining não dão suporte a **$ProbabilityVariance**. Essa coluna sempre contém 0 para algoritmos do [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
-   **$ProbabilityStdev**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)]os algoritmos de Data Mining não dão suporte a **$ProbabilityStdev**. Essa coluna sempre contém 0 para algoritmos do [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
-   **$AdjustedProbability**  
  
     A coluna **$AdjustedProbability** é uma [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] extensão do [!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB para especificação de mineração de dados.  
  
## <a name="cluster-columns"></a>Colunas cluster  
 O histograma que a função **PredictHistogram** retorna para uma \<referência de coluna de cluster> consiste nas seguintes colunas:  
  
-   **$Cluster** (representa o nome do cluster)  
  
-   **$Distance**  
  
-   **$Probability**  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o estado previsto da coluna Bike Buyer em uma consulta singleton. A consulta também retorna os dois principais Estados mais prováveis do atributo de comprador de bicicletas, com base na probabilidade ajustada obtida com o uso da função **PredictHistogram** .  
  
```  
SELECT  
  [TM Decision Tree].[Bike Buyer],  
  TopCount(PredictHistogram([Bike Buyer]),$AdjustedProbability,3)  
From  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;de cluster &#40;DMX](../dmx/cluster-dmx.md)   
 [&#41;&#40;DMX ClusterProbability](../dmx/clusterprobability-dmx.md)   
 [&#41;&#40;DMX PredictAdjustedProbability](../dmx/predictadjustedprobability-dmx.md)   
 [&#41;&#40;DMX PredictProbability](../dmx/predictprobability-dmx.md)   
 [&#41;&#40;DMX PredictStdev](../dmx/predictstdev-dmx.md)   
 [&#41;&#40;DMX PredictSupport](../dmx/predictsupport-dmx.md)   
 [&#41;&#40;DMX PredictVariance](../dmx/predictvariance-dmx.md)   
 [Algoritmos de mineração de dados &#40;mineração de dados Analysis Services&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [Referência de função&#41; DMX &#40;extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40;&#41;DMX](../dmx/functions-dmx.md)   
 [Funções de previsão gerais &#40;&#41;DMX](../dmx/general-prediction-functions-dmx.md)  
  
  
