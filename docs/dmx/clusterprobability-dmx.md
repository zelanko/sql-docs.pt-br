---
title: ClusterProbability (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 60c95521ba42dc5877c0e10a3f34453a497ad438
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969924"
---
# <a name="clusterprobability-dmx"></a>ClusterProbability (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Retorna a probabilidade de que o caso de entrada pertença ao cluster especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ClusterProbability([<Node_Caption>])  
```  
  
## <a name="applies-to"></a>Aplica-se A  
 Essa função só pode ser usada se o modelo de mineração de dados subjacente oferecer suporte a clustering.  
  
## <a name="return-type"></a>Tipo de retorno  
 Valor escalar.  
  
## <a name="remarks"></a>Comentários  
 A sintaxe a seguir usa o conjunto de linhas do esquema de conteúdo do modelo de mineração para retornar as legendas de nó que existem no modelo de mineração.  
  
```  
SELECT NODE_CAPTION FROM <model>.CONTENT  
```  
  
 Para obter mais informações sobre como usar essa sintaxe, consulte [selecionar do modelo de &#60;&#62;.&#41;de conteúdo &#40;DMX ](../dmx/select-from-model-content-dmx.md). Para obter mais informações sobre o conjunto de linhas do esquema de conteúdo do modelo de mineração, consulte [DMSCHEMA_MINING_MODEL_CONTENT conjunto de linhas](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/ms126267(v=sql.110)).  
  
 Se um \<node caption> não for especificado, a função retornará a probabilidade de que os casos de entrada pertençam ao cluster mais provável. Use a função de **cluster** para retornar o cluster mais provável.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [&#41;de cluster &#40;DMX](../dmx/cluster-dmx.md)   
 [Referência de função&#41; DMX &#40;extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40;&#41;DMX](../dmx/functions-dmx.md)   
 [Funções de previsão gerais &#40;&#41;DMX](../dmx/general-prediction-functions-dmx.md)  
  
  
