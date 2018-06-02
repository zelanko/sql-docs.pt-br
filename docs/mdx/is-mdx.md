---
title: É (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5c36a5f45e34d6d78043f6ce8a3e3fb040ecc9f6
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578588"
---
# <a name="is-mdx"></a>IS (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 Um valor booliano que retorna **true** se ambos os argumentos se referem ao mesmo objeto; caso contrário, **false**. Se o **nulo** palavra-chave for especificado, o operador retornará **true** se *Expression1* é **nulo**; caso contrário, **false**.  
  
## <a name="remarks"></a>Remarks  
 O **IS** operador geralmente é usado para determinar se tuplas e membros são idempotentes, o que significa que eles são precisamente equivalentes.  
  
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
  
  
