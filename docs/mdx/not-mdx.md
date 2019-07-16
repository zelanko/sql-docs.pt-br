---
title: NÃO (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4031b887eb0a42580d6ae8debf6c9177ff67efc3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088230"
---
# <a name="not-mdx"></a>NOT (MDX)


  Realiza uma negação lógica em uma expressão numérica.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Expression1*  
 Uma linguagem MDX válida que retorna um valor numérico.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor booliano que retorna **falsos** se o argumento for avaliado como **verdadeiro**; caso contrário, **verdadeiro**.  
  
## <a name="remarks"></a>Comentários  
 O **não** operador trata a expressão como um valor booliano (zero, 0, como **falso**; caso contrário, **verdadeiro**) antes que o operador realize a negação lógica. A tabela a seguir ilustra como o **não** operador executa a negação lógica.  
  
|*Expression1*|Valor retornado|  
|-------------------|------------------|  
|**true**|**false**|  
|**false**|**true**|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de operador MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
