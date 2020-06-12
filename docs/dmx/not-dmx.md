---
title: NÃO (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 23aaa06f7da6c29cf1f082c27071d68fa0c6958a
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669190"
---
# <a name="not-dmx"></a>NOT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Operador lógico que executa uma negação lógica em uma expressão numérica.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Expression1*  
 Expressão DMX válida que retorna um valor numérico.  
  
## <a name="return-value"></a>Valor Retornado  
 Valor booliano que retorna FALSE se o argumento avaliar como TRUE; do contrário, FALSE.  
  
## <a name="remarks"></a>Comentários  
 O argumento é tratado como valor booliano (0 como FALSE; do contrário, TRUE) antes que o operador realize a negação lógica. Se *expression1* for true, o operador retornará false. Se *expression1* for false, o operador retornará true. A tabela a seguir ilustra como a conjunção lógica é executada.  
  
|Se a Expression1 for|O valor de retorno será|  
|-----------------------|---------------------|  
|VERDADEIRO|FALSO|  
|FALSO|VERDADEIRO|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de operador de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores lógicos &#40;&#41;DMX](../dmx/operators-logical.md)   
 [Operadores &#40;&#41;DMX](../dmx/operators-dmx.md)  
  
  
