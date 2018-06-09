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
manager: kfile
ms.openlocfilehash: d72af1bf0b671eeb2bd4b84c194f129ed1ce6bfe
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34741025"
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
  
## <a name="remarks"></a>Remarks  
 As posições de membros em um nível são determinadas pela ordem natural da hierarquia de atributo. A numeração das posições se baseia em zero.  
  
 Se o lead especificado for zero (0), o **levar** função retorna o membro especificado.  
  
 Se o lead especificado for negativo, o **levar** função retorna um membro anterior.  
  
 `Lead(1)` é equivalente a [NextMember](../mdx/nextmember-mdx.md) função. `Lead(-1)` é equivalente a [PrevMember](../mdx/prevmember-mdx.md) função.  
  
 O **levar** função é semelhante ao [latência](../mdx/lag-mdx.md) funcionar, exceto que o **latência** função procura na direção oposta a **levar** função. Ou seja, `Lead(n)` é equivalente a `Lag(-n)`.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
