---
title: Count (dimensão) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6ee8fe09f7a840d32511d3a208a4621612ee9939
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63285053"
---
# <a name="count-dimension-mdx"></a>Count (Dimensão) (MDX)


  Retorna o número de hierarquias em um cubo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Dimensions.Count   
```  
  
## <a name="remarks"></a>Comentários  
 Retorna o número de hierarquias em um cubo, inclusive a hierarquia `[Measures].[Measures]`.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o número de hierarquias no cubo Adventure Works.  
  
```  
WITH MEMBER measures.X AS  
  dimensions.count   
SELECT Measures.X ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Contagem de &#40;tupla&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [Contagem de &#40;níveis de hierarquia&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Count &#40;Set&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
