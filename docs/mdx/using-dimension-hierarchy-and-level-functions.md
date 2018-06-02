---
title: Usando funções de nível de dimensão e hierarquia | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 96315c01133f3a25e5853ba076d2b28e5ba81a35
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581488"
---
# <a name="using-dimension-hierarchy-and-level-functions"></a>Usando funções de dimensão, hierarquia e nível
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  As funções de dimensão, hierarquia e nível são úteis para desviar as estruturas multidimensionais encontradas no Analysis Services. Geralmente, você usa tais funções junto com outras para obter informações sobre os membros de uma dimensão, hierarquia ou nível.  
  
 O exemplo a seguir mostra como usar o **. Dimensão**, **. Hierarquia**, e **. Nível de** funções:  
  
 `WITH`  
  
 `MEMBER MEASURES.DIMENSIONNAME AS [Date].[Calendar].CURRENTMEMBER.DIMENSION.NAME`  
  
 `MEMBER MEASURES.HIERARCHYNAME AS [Date].[Calendar].CURRENTMEMBER.HIERARCHY.NAME`  
  
 `MEMBER MEASURES.LEVELNAME AS [Date].[Calendar].LEVEL.NAME`  
  
 `SELECT`  
  
 `{MEASURES.DIMENSIONNAME, MEASURES.HIERARCHYNAME, MEASURES.LEVELNAME}`  
  
 `ON Columns,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte também  
 [Dimensão &#40;MDX&#41;](../mdx/dimension-mdx.md)   
 [Funções &#40;sintaxe MDX&#41;](../mdx/functions-mdx-syntax.md)   
 [Hierarquia &#40;MDX&#41;](../mdx/hierarchy-mdx.md)   
 [Nível de &#40;MDX&#41;](../mdx/level-mdx.md)  
  
  
