---
title: '&lt;&gt; (Não igual a) (DMX) | Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7d8a7d790f55e955b92621caa1b1e729486eca19
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008222"
---
# <a name="ltgt-not-equal-to-dmx"></a>&lt;&gt; (Não igual a) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Realiza uma operação de comparação que determina se o valor de uma expressão DMX (Data Mining Extensions) é diferente do valor de outra expressão DMX.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DMX_Expression <> DMX_Expression  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DMX_Expression*  
 Expressão DMX válida.  
  
## <a name="return-value"></a>Valor retornado  
 Valor Booliano que conterá TRUE se ambos os parâmetros forem não nulos e o valor do primeiro parâmetro for diferente do valor do segundo parâmetro. Valor Booliano contendo FALSE se ambos os parâmetros forem não nulos e se o valor do primeiro parâmetro for igual ao valor do segundo parâmetro. O valor Booliano conterá um valor nulo se um ou ambos os parâmetros forem avaliados como um valor nulo.  
  
## <a name="see-also"></a>Consulte também  
 [Operadores de comparação &#40;DMX&#41;](../dmx/operators-comparison.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operators &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
