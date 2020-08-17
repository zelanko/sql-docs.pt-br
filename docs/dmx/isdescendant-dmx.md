---
description: IsDescendant (DMX)
title: IsDescendant (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9fe1c150f243e78c379823427e9940bba3680cb1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88352642"
---
# <a name="isdescendant-dmx"></a>IsDescendant (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Indica se o nó atual descende do nó especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IsDescendant(<NodeID>)  
```  
  
## <a name="return-type"></a>Tipo de retorno  
 Um tipo booleano.  
  
## <a name="remarks"></a>Comentários  
 **IsDescendant** é usado somente no [modelo SELECT do &#60;&#62;. CONTEÚDO &#40;&#41;DMX ](../dmx/select-from-model-content-dmx.md) e [selecione &#60;modelo&#62;. DIMENSION_CONTENT &#40;consultas&#41;DMX ](../dmx/select-from-model-dimension-content-dmx.md) .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna todos os casos que descendem do nó especificado na função IsDescendant.  
  
```  
SELECT * FROM [TM Decision Tree].CONTENT  
WHERE IsDescendant('00000000100')  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função&#41; DMX &#40;extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40;&#41;DMX ](../dmx/functions-dmx.md)   
 [Funções de previsão gerais &#40;&#41;DMX ](../dmx/general-prediction-functions-dmx.md)  
  
  
