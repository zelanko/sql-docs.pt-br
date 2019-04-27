---
title: RangeMid (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8e7daff41d09f1468f3819af5a8d2020719aebe9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62658997"
---
# <a name="rangemid-dmx"></a>RangeMid (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna a parte mediana da partição prevista que é descoberta para a coluna de dados discretos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RangeMid(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>Aplica-se a  
 Colunas de dados discretos escalares.  
  
## <a name="return-type"></a>Tipo de retorno  
 Valor escalar.  
  
## <a name="remarks"></a>Comentários  
 Quando usado com [SELECT FROM &#60;modelo&#62; PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md), o **RangeMin**, **RangeMid**, e **RangeMax**  funções retornam os valores de limite atuais da partição especificada. Por exemplo, se uma previsão for realizada em uma coluna de dados discretos, a consulta retornará o número de partição previsto na coluna de dados discretos. O **RangeMin**, **RangeMid**, e **RangeMax** funções descrevem a partição que especifica a previsão. Quando o **RangeMid** função é usada com uma instrução PREDICTION JOIN, a referência de coluna escalar só pode conter colunas de dados discretas e previsíveis.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna valores mínimo, máximo e médio para a coluna contínua Yearly Income em um modelo de mineração de Árvore de decisão TM.  
  
```  
SELECT DISTINCT   
    RangeMin([Yearly Income]) AS [Bucket Minimum],  
    RangeMid([Yearly Income]) AS [Bucket Average],   
    RangeMax([Yearly Income]) AS [Bucket Maximum]  
FROM [TM Decision Tree]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Functions &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funções de previsão gerais &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)   
 [RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)  
  
  
