---
title: IsAncestor (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ISANCESTOR
dev_langs:
- kbMDX
helpviewer_keywords:
- IsAncestor function
ms.assetid: 49d2fcdf-8d9a-4c79-bd00-4910ea149141
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: eb2d6dcfb4e5d0992a522c060947d942a5b48a53
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="isancestor-mdx"></a>IsAncestor (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 O **IsAncestor** função retorna **true** se o primeiro membro especificado for um ancestral do segundo membro especificado. Caso contrário, a função retorna **false**.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna **true** se [Date]. [ Fiscal]. CurrentMember for um ancestral de janeiro de 2003:  
  
 `WITH MEMBER MEASURES.ISANCESTORDEMO AS`  
  
 `IsAncestor([Date].[Fiscal].CurrentMember, [Date].[Fiscal].[Month].&[2003]&[1])`  
  
 `SELECT MEASURES.ISANCESTORDEMO ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte também  
 [Ancestral &#40; MDX &#41;](../mdx/ancestor-mdx.md)   
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

