---
title: ClusterProbability (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: ClusterProbability
dev_langs: DMX
helpviewer_keywords: ClusterProbability function
ms.assetid: a6447b3c-94ce-4122-a3eb-6f3827598d8f
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 0dfd508ca34f1b2b138087a0386fb1596ef0bc37
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
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
  
 Para obter mais informações sobre como usar essa sintaxe, consulte [SELECT FROM &#60; modelo de &#62;. CONTEÚDO &#40; DMX &#41; ](../dmx/select-from-model-content-dmx.md). Para obter mais informações sobre o conjunto de linhas de esquema de conteúdo de modelo de mineração, consulte [de linhas DMSCHEMA_MINING_MODEL_CONTENT](../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-rowset.md).  
  
 Se um \<legenda de nó > não for especificado, a função retornará a probabilidade de que os casos de entrada pertencem ao cluster mais provável. Use o **Cluster** função para retornar o cluster mais provável.  
  
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
 [Cluster &#40; DMX &#41;](../dmx/cluster-dmx.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [Funções de previsão geral &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
