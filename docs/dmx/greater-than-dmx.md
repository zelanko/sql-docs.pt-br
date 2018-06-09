---
title: '&gt; (Maior que) (DMX) | Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 17c48c5321a0eef25a7fdf3ad0fba5aa643398d4
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34842859"
---
# <a name="gt-greater-than-dmx"></a>&gt; (Maior que) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Realiza uma operação de comparação que determina se o valor de uma expressão DMX (Data Mining Extensions) é maior do que o valor de outra expressão DMX.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DMX_Expression > DMX_Expression  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DMX_Expression*  
 Expressão DMX válida.  
  
## <a name="return-value"></a>Valor retornado  
 Valor booliano que conterá TRUE se ambos os parâmetros forem não nulos e se o primeiro parâmetro tiver um valor maior do que o valor do segundo parâmetro. O valor booliano conterá FALSE se ambos os parâmetros forem não nulos e se o primeiro parâmetro tiver um valor igual a ou menor do que o valor do segundo parâmetro. O valor Booliano conterá um valor nulo se um ou ambos os parâmetros forem avaliados como um valor nulo.  
  
## <a name="see-also"></a>Consulte também  
 [Operadores de comparação &#40;DMX&#41;](../dmx/operators-comparison.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
