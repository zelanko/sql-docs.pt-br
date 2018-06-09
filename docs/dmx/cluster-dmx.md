---
title: Cluster (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 41f835a93e5976945281b6b04258c516b0322236
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34841299"
---
# <a name="cluster-dmx"></a>Cluster (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o cluster com maior probabilidade de conter o caso de entrada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Cluster()  
```  
  
## <a name="applies-to"></a>Aplica-se a  
 Essa função só pode ser usada se o modelo de mineração de dados subjacente oferecer suporte a clustering.  
  
## <a name="return-type"></a>Tipo de retorno  
 O **Cluster** função não requer parâmetros.  
  
 O **Cluster** função retorna um valor escalar de um nome de cluster. No entanto, se você usar essa função como um argumento de outra função, você deve considerá-la como um \<cluster referência de coluna >.  
  
## <a name="remarks"></a>Remarks  
 **Cluster** também pode ser usado como um `<`referência de coluna de cluster`>` para um **PredictHistogram** função.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa uma consulta singleton com o [PredictHistogram &#40;DMX&#41; ](../dmx/predicthistogram-dmx.md) e funções para retornar a distância do caso individual de cada cluster do modelo de mineração de Clustering TM do Cluster e o probabilidade de que o caso individual existirá em cada cluster.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funções de previsão geral &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
