---
title: + Agrega (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 63fe6414d6f1df9f3855c01e0e7f03f523fe3a36
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86971924"
---
# <a name="-add-dmx"></a>+ (Adicionar) (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Realiza uma operação aritmética que adiciona simultaneamente dois números.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Numeric_Expression + Numeric_Expression  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Numeric_Expression*  
 Expressão DMX (Data Mining Extensions) válida que retorna um valor numérico.  
  
## <a name="return-value"></a>Valor Retornado  
 Valor que possui o tipo de dados do parâmetro que tem prioridade alta.  
  
## <a name="remarks"></a>Comentários  
 As duas expressões devem ser do mesmo tipo de dados ou uma expressão deve poder ser convertida implicitamente no tipo de dados da outra expressão. Se uma expressão avaliar a um valor nulo, o operador retornará o resultado da outra expressão.  
  
## <a name="see-also"></a>Consulte Também  
 [Operadores aritméticos &#40;&#41;DMX](../dmx/operators-arithmetic.md)   
 [Referência de operador de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores &#40;&#41;DMX](../dmx/operators-dmx.md)  
  
  
