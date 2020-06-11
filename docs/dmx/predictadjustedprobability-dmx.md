---
title: PredictAdjustedProbability (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 610d304f2634a4de8f8578fff3258f4b1f2dbc67
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669297"
---
# <a name="predictadjustedprobability-dmx"></a>PredictAdjustedProbability (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna a probabilidade ajustada de um estado especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
PredictAdjustedProbability(<scalar column reference>, [<predicted state>])  
```  
  
## <a name="applies-to"></a>Aplica-se A  
 Uma coluna escalar.  
  
## <a name="return-type"></a>Tipo de retorno  
 Valor escalar.  
  
## <a name="remarks"></a>Comentários  
 Se o estado previsto for omitido, o estado que tiver a mais alta probabilidade previsível será usado, excluindo-se a partição de estados faltantes. Para incluir o Bucket de Estados ausentes, defina o \< estado previsto> como **INCLUDE_NULL**.  
  
 Para retornar a probabilidade ajustada para os Estados ausentes, defina o \< estado previsto> como nulo.  
  
 A função **PredictAdjustedProbability** é uma [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] extensão para a [!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB para especificação de mineração de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa uma junção de previsão natural para determinar se um indivíduo é provavelmente um comprador de bicicletas, com base no modelo de mineração da Árvore de decisão TM, e determina também a probabilidade ajustada para a previsão.  
  
```  
SELECT  
  [Bike Buyer],  
  PredictAdjustedProbability([Bike Buyer]) AS [Adjusted Probability]  
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
  
  
