---
title: Referência de função de Data Mining Extensions (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9f0851d3ec373161c9277013fc746ebda5b91f89
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34842529"
---
# <a name="data-mining-extensions-dmx-function-reference"></a>Referência de função de DMX (Data Mining Extensions)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oferece suporte a várias funções da linguagem DMX (Data Mining Extensions). As funções expandem os resultados de uma consulta de previsão para incluir informações que descrevem melhor a previsão. As funções também fornecem mais controle sobre como são retornados os resultados da previsão. A tabela a seguir fornece links para recursos para ajudá-lo a entender como usar funções em DMX.  
  
|Função|Description|  
|--------------|-----------------|  
|[Funções de previsão geral &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)|Lista as funções que podem ser usadas com todos os tipos de modelos e fornece links para mais informações sobre como consultar tipos específicos de modelos de mineração.|  
|[Estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)|Fornece uma visão geral de como construir uma consulta de previsão usando DMX.|  
|[BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)|Retorna uma tabela que contém um número especificado de linhas mais baixas, em ordem crescente de classificação, com base em uma expressão de classificação.|  
  
 A tabela a seguir lista as funções que a DMX suporta.  
  
|Função|Description|  
|--------------|-----------------|  
|[BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)|Retorna uma tabela que contém as últimas linhas de n-item da expressão de tabela, em ordem crescente, com base em uma expressão de classificação.|  
|[BottomPercent &#40;DMX&#41;](../dmx/bottompercent-dmx.md)|Retorna uma tabela que contém o menor número linhas mais baixas, que atendem uma expressão de porcentagem especificada, em ordem crescente de classificação, com base em uma expressão de classificação.|  
|[BottomSum &#40;DMX&#41;](../dmx/bottomsum-dmx.md)|Retorna uma tabela que contém o menor número linhas mais baixas, que atendem uma expressão de soma especificada, em ordem crescente de classificação, com base em uma expressão de classificação.|  
|[Cluster &#40;DMX&#41;](../dmx/cluster-dmx.md)|Retorna o cluster com maior probabilidade de conter o caso de entrada.|  
|[ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)|Retorna a probabilidade de que o caso de entrada pertença ao cluster.|  
|[Existe &#40;DMX&#41;](../dmx/exists-dmx.md)|Retornará true se o conjunto de resultados retornado pela instrução SELECT especificada contiver pelo menos uma linha.|  
|[IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)|Indica se o nó atual descende do nó especificado.|  
|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)|Indica se o nó especificado contém o caso.|  
|[IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md)|Indica se um caso pertence ao conjunto de casos de teste.|  
|[IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)|Indica se um caso pertence ao conjunto de casos de treinamento.|  
|[Latência &#40;DMX&#41;](../dmx/lag-dmx.md)|Retorna a fração de tempo entre a data do caso atual e a última data na data.|  
|[Prever &#40;DMX&#41;](../dmx/predict-dmx.md)|Executa uma previsão em uma coluna especificada.|  
|[PredictAdjustedProbability &#40;DMX&#41;](../dmx/predictadjustedprobability-dmx.md)|Retorna a probabilidade ajustada da coluna previsível especificada.|  
|[PredictAssociation &#40;DMX&#41;](../dmx/predictassociation-dmx.md)|Prevê associação de membro em uma coluna.|  
|[PredictCaseLikelihood &#40;DMX&#41;](../dmx/predictcaselikelihood-dmx.md)|Retorna a probabilidade de que um caso de entrada se ajuste dentro do modelo existente. Essa função só pode ser usada com modelos de clustering.|  
|[PredictHistogram &#40;DMX&#41;](../dmx/predicthistogram-dmx.md)|Retorna uma tabela que representa o histograma para a coluna especificada.|  
|[PredictNodeId &#40;DMX&#41;](../dmx/predictnodeid-dmx.md)|Retorna a Identificação do nó para o caso selecionado.|  
|[PredictProbability &#40;DMX&#41;](../dmx/predictprobability-dmx.md)|Retorna a probabilidade da coluna especificada.|  
|[PredictSequence &#40;DMX&#41;](../dmx/predictsequence-dmx.md)|Prevê os próximos valores em uma sequência.|  
|[PredictStdev &#40;DMX&#41;](../dmx/predictstdev-dmx.md)|Recupera o valor de desvio padrão para uma coluna especificada.|  
|[PredictSupport &#40;DMX&#41;](../dmx/predictsupport-dmx.md)|Retorna o valor de suporte de uma coluna.|  
|[PredictTimeSeries &#40;DMX&#41;](../dmx/predicttimeseries-dmx.md)|Prevê os valores futuros para uma série temporal.|  
|[PredictVariance &#40;DMX&#41;](../dmx/predictvariance-dmx.md)|Retorna o valor de variação da coluna especificada.|  
|[RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)|Retorna o valor superior da partição prevista que é descoberto para a coluna diferenciada especificada.|  
|[RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)|Retorna o valor de ponto central da partição prevista que é descoberta para a coluna diferenciada especificada.|  
|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)|Retorna o valor inferior da partição prevista que é descoberto para a coluna diferenciada especificada.|  
|[StructureColumn &#40;DMX&#41;](../dmx/structurecolumn-dmx.md)|Retorna o valor da coluna de estrutura de mineração de tabela especificada.|  
|[TopCount &#40;DMX&#41;](../dmx/topcount-dmx.md)|Retorna uma tabela que contém um número especificado de linhas mais altas, em ordem decrescente de classificação, com base em uma expressão de classificação.|  
|[TopPercent &#40;DMX&#41;](../dmx/toppercent-dmx.md)|Retorna uma tabela que contém o menor número linhas mais altas que atendem uma expressão de porcentagem especificada, em ordem decrescente de classificação, com base em uma expressão de classificação.|  
|[TopSum &#40;DMX&#41;](../dmx/topsum-dmx.md)|Retorna uma tabela que contém o menor número linhas mais altas que atendem uma expressão de soma especificada, em ordem decrescente de classificação, com base em uma expressão de classificação.|  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40;DMX&#41; referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensões de mineração de dados &#40;DMX&#41; convenções de sintaxe](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensões de mineração de dados &#40;DMX&#41; elementos de sintaxe](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funções de previsão geral &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estrutura e o uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
