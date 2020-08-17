---
description: IsAncestor (MDX)
title: IsAncestor (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ccc61de94c87972eda3dbebdba798f9b1c4028b1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341482"
---
# <a name="isancestor-mdx"></a>IsAncestor (MDX)


  Retorna se um membro especificado é um ancestral de outro membro especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IsAncestor(Member_Expression1, Member_Expression2)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression1*  
 Uma linguagem MDX válida que retorna um membro.  
  
 *Member_Expression2*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Comentários  
 A função **IsAncestor** retornará **true** se o primeiro membro especificado for um ancestral do segundo membro especificado. Caso contrário, a função retornará **false**.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retornará **true** se [date]. [Fiscal]. CurrentMember é um ancestral de janeiro de 2003:  
  
 `WITH MEMBER MEASURES.ISANCESTORDEMO AS`  
  
 `IsAncestor([Date].[Fiscal].CurrentMember, [Date].[Fiscal].[Month].&[2003]&[1])`  
  
 `SELECT MEASURES.ISANCESTORDEMO ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;ancestral &#40;MDX ](../mdx/ancestor-mdx.md)   
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
