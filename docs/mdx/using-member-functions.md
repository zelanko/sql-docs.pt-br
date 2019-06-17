---
title: Usando funções de membro | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1c9979b6b9fcb04115695cbe8d9c224e1c6c1f57
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63251602"
---
# <a name="using-member-functions"></a>Usando as funções de membro


  Uma função de membro é uma função MDX válida que retorna um membro. As funções de membro, assim como as funções de tupla e de conjunto, são essenciais para negociar as estruturas multidimensionais encontradas no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 De muitas funções de membro em MDX, o mais importante é o **CurrentMember** função, que é usada para determinar o membro atual em uma hierarquia. A consulta a seguir ilustra como usá-lo, junto com o **pai**, **ancestral**, e **Prevmember** funções:  
  
 `WITH`  
  
 `//Returns the name of the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[CurrentMemberDemo] AS [Date].[Calendar].CurrentMember.Name`  
  
 `//Returns the name of the parent of the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[ParentDemo] AS [Date].[Calendar].CurrentMember.Parent.Name`  
  
 `//Returns the name of the ancestor of the currentmember on the Calendar hierarchy at the Year level`  
  
 `MEMBER MEASURES.[AncestorDemo] AS ANCESTOR([Date].[Calendar].CurrentMember, [Date].[Calendar].[Calendar Year]).Name`  
  
 `//Returns the name of the member before the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[PrevMemberDemo] AS [Date].[Calendar].CurrentMember.Prevmember.Name`  
  
 `SELECT{MEASURES.[CurrentMemberDemo],MEASURES.[ParentDemo],MEASURES.[AncestorDemo],MEASURES.[PrevMemberDemo] } ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte também  
 [Funções &#40;sintaxe MDX&#41;](../mdx/functions-mdx-syntax.md)   
 [Usando funções de tupla](../mdx/using-tuple-functions.md)   
 [Usando funções de conjunto](../mdx/using-set-functions.md)  
  
  
