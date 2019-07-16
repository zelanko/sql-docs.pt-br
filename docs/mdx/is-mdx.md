---
title: É (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: aaf4151d8291ccd4249892c6ef8fce8a3d280f6b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905978"
---
# <a name="is-mdx"></a>IS (MDX)


  Executa uma comparação lógica em duas expressões de objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Expression1 IS ( Expression2 | NULL )  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Expression1*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna uma referência de objeto MDX.  
  
 *Expression2*  
 Uma expressão MDX válida que retorna uma referência de objeto MDX.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor booliano que retorna **verdadeira** se ambos os argumentos se referirem ao mesmo objeto; caso contrário, **falso**. Se o **nulo** palavra-chave for especificado, o operador retorna **verdadeiro** se *Expression1* é **nulo**; caso contrário, **false** .  
  
## <a name="remarks"></a>Comentários  
 O **IS** é frequentemente usado para determinar se tuplas e membros são idempotentes, que significa que eles são exatamente equivalentes.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como usar o **IS** operador para verificar se o membro atual em um eixo é um membro específico:  
  
 `With`  
  
 `//Returns TRUE if the currentmember is Bikes`  
  
 `Member [Measures].[IsBikes?] AS`  
  
 `[Product].[Category].CurrentMember IS [Product].[Category].&[1]`  
  
 `SELECT`  
  
 `{[Measures].[IsBikes?]} ON 0,`  
  
 `[Product].[Category].[Category].Members ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
## <a name="see-also"></a>Consulte também  
 [Referência de operador MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
