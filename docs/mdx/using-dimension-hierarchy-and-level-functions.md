---
title: "Usando funções de nível de dimensão e hierarquia | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords:
- dimensions [Analysis Services], functions
- level functions [MDX]
- hierarchy functions [MDX]
ms.assetid: e730f65a-1798-4094-9acf-2739e2505d52
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 95264cc1e894fdd2acd43b4f49807968ea9ce587
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
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
  
## <a name="see-also"></a>Consulte Também  
 [Dimensão &#40; MDX &#41;](../mdx/dimension-mdx.md)   
 [Funções &#40; Sintaxe MDX &#41;](../mdx/functions-mdx-syntax.md)   
 [Hierarquia de &#40; MDX &#41;](../mdx/hierarchy-mdx.md)   
 [Nível &#40; MDX &#41;](../mdx/level-mdx.md)  
  
  
