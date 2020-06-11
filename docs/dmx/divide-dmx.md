---
title: Dividir (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2d75bd4a1d4b75d9acb153c3a3aec9efcf58d876
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669745"
---
# <a name="divide-dmx"></a>(Dividir) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Realiza uma operação aritmética que divide um número por outro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Dividend / Divisor  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Cheque*  
 Expressão DMX (Data Mining Extensions) válida que retorna um valor numérico.  
  
 *Divisor*  
 Expressão DMX válida que retorna um valor numérico.  
  
## <a name="return-value"></a>Valor Retornado  
 Valor que possui o tipo de dados do parâmetro que tem prioridade alta.  
  
## <a name="remarks"></a>Comentários  
 O valor que esse operador retorna representa o quociente da primeira expressão dividido pela segunda expressão.  
  
 As duas expressões devem ser do mesmo tipo de dados ou uma expressão deve poder ser convertida implicitamente no tipo de dados da outra expressão. Se o divisor avaliar um valor nulo, o operador apresentará um erro. Se ambos, o divisor e o dividendo avaliarem um valor nulo, o operador retornará um valor nulo.  
  
## <a name="see-also"></a>Consulte Também  
 [Operadores aritméticos &#40;&#41;DMX](../dmx/operators-arithmetic.md)   
 [Referência de operador de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores &#40;&#41;DMX](../dmx/operators-dmx.md)   
 [Dividir &#40;expressão SSIS&#41;](../integration-services/expressions/divide-ssis-expression.md)   
 [&#40;dividir&#41; &#40;Transact-SQL&#41;](../t-sql/language-elements/divide-transact-sql.md)  
  
  
