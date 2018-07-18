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
manager: kfile
ms.openlocfilehash: 4a57d0b1c7f1fa75504e786712029326fc958135
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38023844"
---
# <a name="or-dmx"></a>OR (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Operador lógico que executa uma disjunção lógica em duas expressões numéricas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Expression1 OR Expression2  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Expression1*  
 Expressão DMX (Data Mining Extensions) válida que retorna um valor numérico.  
  
 *Expression2*  
 Expressão DMX válida que retorna um valor numérico.  
  
## <a name="return-value"></a>Valor retornado  
 Valor booliano que retorna TRUE quando um argumento ou todos os argumentos avaliarem TRUE; do contrário, FALSE.  
  
## <a name="remarks"></a>Remarks  
 Os argumentos são todos tratados como valores boolianos (0 como FALSE; do contrário, TRUE) antes que o operador realize a disjunção lógica. Se um ou ambos os argumentos forem avaliados como TRUE, o operador retornará TRUE. Se *Expression1* é avaliada como TRUE e *Expression2* for avaliada como FALSE, o operador retornará TRUE.  
  
 A tabela a seguir ilustra como a disjunção lógica é executada.  
  
|Se a Expression1 for|Se a Expression2 for|O valor de retorno será|  
|-----------------------|-----------------------|---------------------|  
|TRUE|TRUE|TRUE|  
|TRUE|FALSE|TRUE|  
|FALSE|TRUE|TRUE|  
|FALSE|FALSE|FALSE|  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40;DMX&#41; referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores lógicos &#40;DMX&#41;](../dmx/operators-logical.md)   
 [Operadores &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
