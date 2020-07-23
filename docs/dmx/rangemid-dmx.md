---
title: RangeMid (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e3f13f1d110c26ee590df3a09296f6d861e34e37
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970649"
---
# <a name="rangemid-dmx"></a>RangeMid (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Retorna a parte mediana da partição prevista que é descoberta para a coluna de dados discretos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RangeMid(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>Aplica-se A  
 Colunas de dados discretos escalares.  
  
## <a name="return-type"></a>Tipo de retorno  
 Valor escalar.  
  
## <a name="remarks"></a>Comentários  
 Quando usado com [Select do modelo de &#60;&#62; junção de previsão &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md), as funções **RangeMin**, **RangeMid**e **RangeMax** retornam os valores de limite reais do Bucket especificado. Por exemplo, se uma previsão for realizada em uma coluna de dados discretos, a consulta retornará o número de partição previsto na coluna de dados discretos. As funções **RangeMin**, **RangeMid**e **RangeMax** descrevem o Bucket que a previsão especifica. Quando a função **RangeMid** é usada com uma instrução de junção de previsão, a referência de coluna escalar pode conter apenas colunas discretas e previsíveis.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna valores mínimo, máximo e médio para a coluna contínua Yearly Income em um modelo de mineração de Árvore de decisão TM.  
  
```  
SELECT DISTINCT   
    RangeMin([Yearly Income]) AS [Bucket Minimum],  
    RangeMid([Yearly Income]) AS [Bucket Average],   
    RangeMax([Yearly Income]) AS [Bucket Maximum]  
FROM [TM Decision Tree]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função&#41; DMX &#40;extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40;&#41;DMX](../dmx/functions-dmx.md)   
 [Funções de previsão gerais &#40;&#41;DMX](../dmx/general-prediction-functions-dmx.md)   
 [&#41;&#40;DMX RangeMax](../dmx/rangemax-dmx.md)   
 [&#41;&#40;DMX RangeMin](../dmx/rangemin-dmx.md)  
  
  
