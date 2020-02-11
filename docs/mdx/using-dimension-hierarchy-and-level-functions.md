---
title: Usando funções de dimensão, hierarquia e nível | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8fa374ef93f56f8cddaed81bc9e3872d1eb206c7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68097186"
---
# <a name="using-dimension-hierarchy-and-level-functions"></a>Usando funções de dimensão, hierarquia e nível


  As funções de dimensão, hierarquia e nível são úteis para desviar as estruturas multidimensionais encontradas no Analysis Services. Geralmente, você usa tais funções junto com outras para obter informações sobre os membros de uma dimensão, hierarquia ou nível.  
  
 O exemplo a seguir mostra como usar o **. Dimensão**, **. Hierarquia**e **. **Funções de nível:  
  
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
 [&#41;de dimensão &#40;MDX](../mdx/dimension-mdx.md)   
 [Funções &#40;sintaxe MDX&#41;](../mdx/functions-mdx-syntax.md)   
 [&#41;de &#40;MDX de hierarquia](../mdx/hierarchy-mdx.md)   
 [&#41;de &#40;MDX de nível](../mdx/level-mdx.md)  
  
  
