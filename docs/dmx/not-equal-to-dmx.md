---
title: '&lt;&gt;(Diferente de) (DMX) | Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1181e781da0e752cb68f0fbf1d8c84d257407a3e
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86968461"
---
# <a name="ltgt-not-equal-to-dmx"></a>&lt;&gt;(Diferente de) Symmetrix
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Realiza uma operação de comparação que determina se o valor de uma expressão DMX (Data Mining Extensions) é diferente do valor de outra expressão DMX.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DMX_Expression <> DMX_Expression  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DMX_Expression*  
 Expressão DMX válida.  
  
## <a name="return-value"></a>Valor Retornado  
 Valor Booliano que conterá TRUE se ambos os parâmetros forem não nulos e o valor do primeiro parâmetro for diferente do valor do segundo parâmetro. Valor Booliano contendo FALSE se ambos os parâmetros forem não nulos e se o valor do primeiro parâmetro for igual ao valor do segundo parâmetro. O valor Booliano conterá um valor nulo se um ou ambos os parâmetros forem avaliados como um valor nulo.  
  
## <a name="see-also"></a>Consulte Também  
 [Operadores de comparação &#40;&#41;DMX](../dmx/operators-comparison.md)   
 [Referência de operador de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores &#40;&#41;DMX](../dmx/operators-dmx.md)  
  
  
