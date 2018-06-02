---
title: Count (dimensão) (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fd8d61e7907a8fb05a016dabdcb65201bffdbbdc
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34577638"
---
# <a name="count-dimension-mdx"></a>Count (Dimensão) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o número de hierarquias em um cubo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Dimensions.Count   
```  
  
## <a name="remarks"></a>Remarks  
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
 [Contagem de &#40;definir&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
