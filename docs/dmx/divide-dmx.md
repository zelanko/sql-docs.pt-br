---
title: (Divisão) (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8ab2b355c551b868cec3ee4329460f8bb0532236
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34842369"
---
# <a name="divide-dmx"></a>(Divisão) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Realiza uma operação aritmética que divide um número por outro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Dividend / Divisor  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *dividendo*  
 Expressão DMX (Data Mining Extensions) válida que retorna um valor numérico.  
  
 *divisor*  
 Expressão DMX válida que retorna um valor numérico.  
  
## <a name="return-value"></a>Valor retornado  
 Valor que possui o tipo de dados do parâmetro que tem prioridade alta.  
  
## <a name="remarks"></a>Remarks  
 O valor que esse operador retorna representa o quociente da primeira expressão dividido pela segunda expressão.  
  
 As duas expressões devem ser do mesmo tipo de dados ou uma expressão deve poder ser convertida implicitamente no tipo de dados da outra expressão. Se o divisor avaliar um valor nulo, o operador apresentará um erro. Se ambos, o divisor e o dividendo avaliarem um valor nulo, o operador retornará um valor nulo.  
  
## <a name="see-also"></a>Consulte também  
 [Operadores aritméticos &#40;DMX&#41;](../dmx/operators-arithmetic.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores &#40;DMX&#41;](../dmx/operators-dmx.md)   
 [Dividir &#40;expressão SSIS&#41;](../integration-services/expressions/divide-ssis-expression.md)   
 [&#40;Dividir&#41; &#40;Transact-SQL&#41;](../t-sql/language-elements/divide-transact-sql.md)  
  
  
