---
title: OU (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 76b1f8ac9a5f7ad584f42110f2c3b22e5c1918ff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68008146"
---
# <a name="or-dmx"></a>OR (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Operador lógico que executa uma disjunção lógica em duas expressões numéricas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Expression1 OR Expression2  
```  
  
#### <a name="parameters"></a>parâmetros  
 *Expression1*  
 Expressão DMX (Data Mining Extensions) válida que retorna um valor numérico.  
  
 *Expression2*  
 Expressão DMX válida que retorna um valor numérico.  
  
## <a name="return-value"></a>Valor retornado  
 Valor booliano que retorna TRUE quando um argumento ou todos os argumentos avaliarem TRUE; do contrário, FALSE.  
  
## <a name="remarks"></a>Comentários  
 Os argumentos são todos tratados como valores boolianos (0 como FALSE; do contrário, TRUE) antes que o operador realize a disjunção lógica. Se um ou ambos os argumentos forem avaliados como TRUE, o operador retornará TRUE. Se *expressão1* for avaliada como true e *expression2* for avaliada como false, o operador retornará true.  
  
 A tabela a seguir ilustra como a disjunção lógica é executada.  
  
|Se a Expression1 for|Se a Expression2 for|O valor de retorno será|  
|-----------------------|-----------------------|---------------------|  
|TRUE|TRUE|TRUE|  
|TRUE|FALSE|TRUE|  
|FALSE|TRUE|TRUE|  
|FALSE|FALSE|FALSE|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de operador de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores lógicos &#40;&#41;DMX](../dmx/operators-logical.md)   
 [Operadores &#40;&#41;DMX](../dmx/operators-dmx.md)  
  
  
