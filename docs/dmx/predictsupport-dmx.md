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
ms.openlocfilehash: 701d8fb43b468f6bbd33fbff9ff7cfc8deb386f9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68893831"
---
# <a name="predictsupport-dmx"></a>PredictSupport (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o valor de suporte para um estado especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
PredictSupport(<scalar column reference>, [<predicted state>])  
```  
  
## <a name="applies-to"></a>Aplica-se A  
 Uma coluna escalar.  
  
## <a name="return-type"></a>Tipo de retorno  
 Um valor escalar do tipo especificado pela referência *\<**>* de coluna escalar.  
  
## <a name="remarks"></a>Comentários  
 Se o estado previsto for omitido, o estado que tiver a mais alta probabilidade previsível será usado, excluindo-se a partição de estados faltantes. Para incluir o Bucket de Estados ausentes, \<defina o estado previsto> como **INCLUDE_NULL**.  
  
 Para retornar o suporte para os Estados ausentes, defina \<o estado previsto> como nulo.  
  
> [!NOTE]  
>  Os valores de suporte são calculados de modo diferente ou talvez tenham uma interpretação diferente dependendo do tipo de modelo que você está consultando. Para obter mais informações sobre como o suporte é calculado para qualquer tipo de modelo específico, consulte o tipo de algoritmo individual no [conteúdo do modelo de mineração &#40;Analysis Services&#41;de mineração de dados ](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-analysis-services-data-mining).  
  
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
 [Funções &#40;&#41;DMX](../dmx/functions-dmx.md)   
 [Funções de previsão gerais &#40;&#41;DMX](../dmx/general-prediction-functions-dmx.md)  
  
  
