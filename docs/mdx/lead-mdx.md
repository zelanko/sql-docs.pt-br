---
title: Cliente potencial (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cc4d362fbc7656e9427548a352b32d5d8297071e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905738"
---
# <a name="lead-mdx"></a>Lead (MDX)


  Retorna o membro que é um número especificado de posições que seguem um membro especificado junto ao nível do membro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Member_Expression.Lead( Index )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
 *Index*  
 Uma expressão numérica válida que especifica várias posições de membro.  
  
## <a name="remarks"></a>Comentários  
 As posições de membros em um nível são determinadas pela ordem natural da hierarquia de atributo. A numeração das posições se baseia em zero.  
  
 Se o cliente potencial especificado for zero (0), a função **Lead** retornará o membro especificado.  
  
 Se o cliente potencial especificado for negativo, a função **Lead** retornará um membro anterior.  
  
 `Lead(1)`é equivalente à função [NextMember](../mdx/nextmember-mdx.md) . `Lead(-1)`é equivalente à função [PrevMember](../mdx/prevmember-mdx.md) .  
  
 A função **Lead** é semelhante à função [lag](../mdx/lag-mdx.md) , exceto que a função **lag** procura na direção oposta à função **Lead** . Ou seja, `Lead(n)` é equivalente a `Lag(-n)`.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o valor para dezembro de 2001:  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lead(-2) ON 0  
FROM [Adventure Works]  
  
```  
  
 O exemplo a seguir retorna o valor para março de 2002:  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lead(1) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
