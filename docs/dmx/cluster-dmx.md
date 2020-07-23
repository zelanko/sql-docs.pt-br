---
title: Cluster (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0cd7b2e0a78f2d47349de2701572b2f9dc4b0095
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969917"
---
# <a name="cluster-dmx"></a>Cluster (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Retorna o cluster com maior probabilidade de conter o caso de entrada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Cluster()  
```  
  
## <a name="applies-to"></a>Aplica-se A  
 Essa função só pode ser usada se o modelo de mineração de dados subjacente oferecer suporte a clustering.  
  
## <a name="return-type"></a>Tipo de retorno  
 A função de **cluster** não requer parâmetros.  
  
 A função **cluster** retorna um valor escalar de um nome de cluster. No entanto, se você usar essa função como um argumento de outra função, deverá considerar isso como uma \<cluster column reference> .  
  
## <a name="remarks"></a>Comentários  
 O **cluster** também pode ser usado como uma `<` referência `>` de coluna de cluster para uma função **PredictHistogram** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa uma consulta singleton com as funções de cluster e de [&#41;de PredictHistogram &#40;DMX](../dmx/predicthistogram-dmx.md) para retornar a distância do caso individual de cada cluster do modelo de mineração de clustering TM e a probabilidade de que o caso individual exista em cada cluster.  
  
```  
SELECT  
  PredictHistogram(Cluster())  
FROM  
  [TM Clustering]  
  NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;DMX ClusterProbability](../dmx/clusterprobability-dmx.md)   
 [Referência de função&#41; DMX &#40;extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40;&#41;DMX](../dmx/functions-dmx.md)   
 [Funções de previsão gerais &#40;&#41;DMX](../dmx/general-prediction-functions-dmx.md)  
  
  
