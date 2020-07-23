---
title: Referência da função DMX (extensões de mineração de dados) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7b25146ce36a0b58bb46bcacb4348f8e34221068
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86971795"
---
# <a name="data-mining-extensions-dmx-function-reference"></a>Referência de função de DMX (Data Mining Extensions)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oferece suporte a várias funções da linguagem DMX (Data Mining Extensions). As funções expandem os resultados de uma consulta de previsão para incluir informações que descrevem melhor a previsão. As funções também fornecem mais controle sobre como são retornados os resultados da previsão. A tabela a seguir fornece links para recursos para ajudá-lo a entender como usar funções em DMX.  
  
|Função|Descrição|  
|--------------|-----------------|  
|[Funções de previsão gerais &#40;&#41;DMX](../dmx/general-prediction-functions-dmx.md)|Lista as funções que podem ser usadas com todos os tipos de modelos e fornece links para mais informações sobre como consultar tipos específicos de modelos de mineração.|  
|[Estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)|Fornece uma visão geral de como construir uma consulta de previsão usando DMX.|  
|[&#41;&#40;DMX BottomCount](../dmx/bottomcount-dmx.md)|Retorna uma tabela que contém um número especificado de linhas mais baixas, em ordem crescente de classificação, com base em uma expressão de classificação.|  
  
 A tabela a seguir lista as funções que a DMX suporta.  
  
|Função|Descrição|  
|--------------|-----------------|  
|[&#41;&#40;DMX BottomCount](../dmx/bottomcount-dmx.md)|Retorna uma tabela que contém as últimas linhas de n-item da expressão de tabela, em ordem crescente, com base em uma expressão de classificação.|  
|[&#41;&#40;DMX BottomPercent](../dmx/bottompercent-dmx.md)|Retorna uma tabela que contém o menor número linhas mais baixas, que atendem uma expressão de porcentagem especificada, em ordem crescente de classificação, com base em uma expressão de classificação.|  
|[&#41;&#40;DMX BottomSum](../dmx/bottomsum-dmx.md)|Retorna uma tabela que contém o menor número linhas mais baixas, que atendem uma expressão de soma especificada, em ordem crescente de classificação, com base em uma expressão de classificação.|  
|[Cluster &#40;DMX&#41;](../dmx/cluster-dmx.md)|Retorna o cluster com maior probabilidade de conter o caso de entrada.|  
|[ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)|Retorna a probabilidade de que o caso de entrada pertença ao cluster.|  
|[Existe &#40;DMX&#41;](../dmx/exists-dmx.md)|Retornará true se o conjunto de resultados retornado pela instrução SELECT especificada contiver pelo menos uma linha.|  
|[IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)|Indica se o nó atual descende do nó especificado.|  
|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)|Indica se o nó especificado contém o caso.|  
|[&#41;&#40;DMX IsTestCase](../dmx/istestcase-dmx.md)|Indica se um caso pertence ao conjunto de casos de teste.|  
|[&#41;&#40;DMX IsTrainingCase](../dmx/istrainingcase-dmx.md)|Indica se um caso pertence ao conjunto de casos de treinamento.|  
|[Lag &#40;DMX&#41;](../dmx/lag-dmx.md)|Retorna a fração de tempo entre a data do caso atual e a última data na data.|  
|[Prever &#40;DMX&#41;](../dmx/predict-dmx.md)|Executa uma previsão em uma coluna especificada.|  
|[PredictAdjustedProbability &#40;DMX&#41;](../dmx/predictadjustedprobability-dmx.md)|Retorna a probabilidade ajustada da coluna previsível especificada.|  
|[PredictAssociation &#40;DMX&#41;](../dmx/predictassociation-dmx.md)|Prevê associação de membro em uma coluna.|  
|[PredictCaseLikelihood &#40;DMX&#41;](../dmx/predictcaselikelihood-dmx.md)|Retorna a probabilidade de que um caso de entrada caiba no modelo existente. Essa função só pode ser usada com modelos de clustering.|  
|[PredictHistogram &#40;DMX&#41;](../dmx/predicthistogram-dmx.md)|Retorna uma tabela que representa o histograma para a coluna especificada.|  
|[PredictNodeId &#40;DMX&#41;](../dmx/predictnodeid-dmx.md)|Retorna a Identificação do nó para o caso selecionado.|  
|[PredictProbability &#40;DMX&#41;](../dmx/predictprobability-dmx.md)|Retorna a probabilidade da coluna especificada.|  
|[PredictSequence &#40;DMX&#41;](../dmx/predictsequence-dmx.md)|Prevê os próximos valores em uma sequência.|  
|[PredictStdev &#40;DMX&#41;](../dmx/predictstdev-dmx.md)|Recupera o valor de desvio padrão para uma coluna especificada.|  
|[PredictSupport &#40;DMX&#41;](../dmx/predictsupport-dmx.md)|Retorna o valor de suporte de uma coluna.|  
|[PredictTimeSeries &#40;DMX&#41;](../dmx/predicttimeseries-dmx.md)|Prevê os valores futuros para uma série temporal.|  
|[PredictVariance &#40;DMX&#41;](../dmx/predictvariance-dmx.md)|Retorna o valor de variação da coluna especificada.|  
|[&#41;&#40;DMX RangeMax](../dmx/rangemax-dmx.md)|Retorna o valor superior da partição prevista que é descoberto para a coluna diferenciada especificada.|  
|[&#41;&#40;DMX RangeMid](../dmx/rangemid-dmx.md)|Retorna o valor de ponto central da partição prevista que é descoberta para a coluna diferenciada especificada.|  
|[&#41;&#40;DMX RangeMin](../dmx/rangemin-dmx.md)|Retorna o valor inferior da partição prevista que é descoberto para a coluna diferenciada especificada.|  
|[&#41;&#40;DMX StructureColumn](../dmx/structurecolumn-dmx.md)|Retorna o valor da coluna de estrutura de mineração de tabela especificada.|  
|[&#41;&#40;DMX TopCount](../dmx/topcount-dmx.md)|Retorna uma tabela que contém um número especificado de linhas mais altas, em ordem decrescente de classificação, com base em uma expressão de classificação.|  
|[&#41;&#40;DMX TopPercent](../dmx/toppercent-dmx.md)|Retorna uma tabela que contém o menor número linhas mais altas que atendem uma expressão de porcentagem especificada, em ordem decrescente de classificação, com base em uma expressão de classificação.|  
|[TopSum &#40;&#41;DMX](../dmx/topsum-dmx.md)|Retorna uma tabela que contém o menor número linhas mais altas que atendem uma expressão de soma especificada, em ordem decrescente de classificação, com base em uma expressão de classificação.|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de operador de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Referência de instrução&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)   
 [&#40;as convenções de sintaxe de&#41; DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [As extensões de mineração de dados &#40;elementos de sintaxe DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funções de previsão gerais &#40;&#41;DMX](../dmx/general-prediction-functions-dmx.md)   
 [Estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
