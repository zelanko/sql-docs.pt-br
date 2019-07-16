---
title: ClusterProbability (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9beac713ec9a8b5a549602809d3612e4e29e67c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071950"
---
# <a name="clusterprobability-dmx"></a>ClusterProbability (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna a probabilidade de que o caso de entrada pertença ao cluster especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ClusterProbability([<Node_Caption>])  
```  
  
## <a name="applies-to"></a>Aplica-se a  
 Essa função só pode ser usada se o modelo de mineração de dados subjacente oferecer suporte a clustering.  
  
## <a name="return-type"></a>Tipo de retorno  
 Valor escalar.  
  
## <a name="remarks"></a>Comentários  
 A sintaxe a seguir usa o conjunto de linhas do esquema de conteúdo do modelo de mineração para retornar as legendas de nó que existem no modelo de mineração.  
  
```  
SELECT NODE_CAPTION FROM <model>.CONTENT  
```  
  
 Para obter mais informações sobre como usar essa sintaxe, consulte [SELECT FROM &#60;modelo&#62;. CONTEÚDO &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md). Para obter mais informações sobre o conjunto de linhas de esquema de conteúdo de modelo de mineração, consulte [conjunto de linhas DMSCHEMA_MINING_MODEL_CONTENT](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset).  
  
 Se um \<legenda de nó > não for especificado, a função retorna a probabilidade de que os casos de entrada pertencem ao cluster mais provável. Use o **Cluster** função para retornar o cluster mais provável.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a probabilidade de que caso especificado exista no cluster rotulado de Cluster 2.  
  
```  
SELECT  
  ClusterProbability('Cluster 2')  
From  
  [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>Consulte também  
 [Cluster &#40;DMX&#41;](../dmx/cluster-dmx.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funções de previsão gerais &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
