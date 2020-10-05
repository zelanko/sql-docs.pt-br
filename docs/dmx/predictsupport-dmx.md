---
description: PredictSupport (DMX)
title: PredictSupport (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 180375f77251adaab9a8d30462267b043ed6e946
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727673"
---
# <a name="predictsupport-dmx"></a>PredictSupport (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Retorna o valor de suporte para um estado especificado.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
PredictSupport(<scalar column reference>, [<predicted state>])  
```  
  
## <a name="applies-to"></a>Aplica-se A  
 Uma coluna escalar.  
  
## <a name="return-type"></a>Tipo de retorno  
 Um valor escalar do tipo especificado por *\<*scalar column reference*>* .  
  
## <a name="remarks"></a>Comentários  
 Se o estado previsto for omitido, o estado que tiver a mais alta probabilidade previsível será usado, excluindo-se a partição de estados faltantes. Para incluir o Bucket de Estados ausentes, defina \<predicted state> como **INCLUDE_NULL**.  
  
 Para retornar o suporte para os Estados ausentes, defina \<predicted state> como NULL.  
  
> [!NOTE]  
>  Os valores de suporte são calculados de modo diferente ou talvez tenham uma interpretação diferente dependendo do tipo de modelo que você está consultando. Para obter mais informações sobre como o suporte é calculado para qualquer tipo de modelo específico, consulte o tipo de algoritmo individual no [conteúdo do modelo de mineração &#40;Analysis Services&#41;de mineração de dados ](/analysis-services/data-mining/mining-model-content-analysis-services-data-mining).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa uma consulta singleton para prever se um indivíduo será um comprador de bicicletas, e também determina o suporte para a previsão com base no modelo de mineração da Árvore de decisão TM.  
  
```  
SELECT  
  [Bike Buyer],  
  PredictSupport([Bike Buyer]) AS [Support],  
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
 [Referência de função&#41; DMX &#40;extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40;&#41;DMX ](../dmx/functions-dmx.md)   
 [Funções de previsão gerais &#40;&#41;DMX ](../dmx/general-prediction-functions-dmx.md)  
  
