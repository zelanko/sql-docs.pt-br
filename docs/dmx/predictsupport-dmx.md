---
title: PredictSupport (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: efe9fb0222dc745e48c248214c42ce706ea18d89
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041875"
---
# <a name="predictsupport-dmx"></a>PredictSupport (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o valor de suporte para um estado especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
PredictSupport(<scalar column reference>, [<predicted state>])  
```  
  
## <a name="applies-to"></a>Aplica-se a  
 Uma coluna escalar.  
  
## <a name="return-type"></a>Tipo de retorno  
 Um valor escalar do tipo especificado pelo *\<* referência de coluna escalar *>* .  
  
## <a name="remarks"></a>Comentários  
 Se o estado previsto for omitido, o estado que tiver a mais alta probabilidade previsível será usado, excluindo-se a partição de estados faltantes. Para incluir a partição de estados faltantes, defina as \<estado previsto > para **INCLUDE_NULL**.  
  
 Para retornar o suporte para os estados faltantes, defina o \<estado previsto > como NULL.  
  
> [!NOTE]  
>  Os valores de suporte são calculados de modo diferente ou talvez tenham uma interpretação diferente dependendo do tipo de modelo que você está consultando. Para obter mais informações sobre como o suporte é calculado para qualquer tipo de modelo específico, consulte o algoritmo individual digitar [conteúdo do modelo de mineração &#40;Analysis Services - mineração de dados&#41;](../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funções de previsão gerais &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
