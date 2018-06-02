---
title: Usando funções de membro | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 59be2bef7e2a3fb57b720672c3c89d0500feef8b
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581548"
---
# <a name="using-member-functions"></a>Usando as funções de membro
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Uma função de membro é uma função MDX válida que retorna um membro. As funções de membro, assim como as funções de tupla e de conjunto, são essenciais para negociar as estruturas multidimensionais encontradas no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 De muitas funções de membro em MDX, o mais importante é o **CurrentMember** função, que é usada para determinar o membro atual em uma hierarquia. A consulta a seguir ilustra como usá-lo, juntamente com o **pai**, **ancestral**, e **Prevmember** funções:  
  
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
  
  
