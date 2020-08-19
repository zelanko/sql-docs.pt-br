---
description: Count (Dimensão) (MDX)
title: Contagem (dimensão) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: afa58c330210e4fdb34d13892101e210f54cd3bd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429958"
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
  
## <a name="see-also"></a>Consulte Também  
 [Contar &#40;tupla&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [Contar &#40;níveis de hierarquia&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Contagem &#40;definida&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
