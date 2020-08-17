---
description: '&gt;= (Maior ou igual a) (DMX)'
title: '&gt;= (Maior ou igual a) (DMX) | Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c34473ee7d8334ae332ce71bc44f94bcfdaee598
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88353072"
---
# <a name="gt-greater-than-or-equal-to-dmx"></a>&gt;= (Maior ou igual a) (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Realiza uma operação de comparação que determina se o valor de uma expressão DMX (Data Mining Extensions) é maior do que ou igual ao valor de outra expressão DMX.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DMX_Expression >= DMX_Expression  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DMX_Expression*  
 Expressão DMX válida.  
  
## <a name="return-value"></a>Valor de retorno  
 Valor booliano que conterá TRUE se ambos os parâmetros forem não nulos e o valor do primeiro parâmetro for maior do que ou igual ao valor do segundo parâmetro. Valor Booliano contendo FALSE se ambos os parâmetros forem não nulos e se o valor do primeiro parâmetro for menor do que o valor do segundo parâmetro. O valor Booliano conterá um valor nulo se um ou ambos os parâmetros forem avaliados como um valor nulo.  
  
## <a name="see-also"></a>Consulte Também  
 [Operadores de comparação &#40;&#41;DMX ](../dmx/operators-comparison.md)   
 [Referência de operador de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores &#40;&#41;DMX ](../dmx/operators-dmx.md)  
  
  
