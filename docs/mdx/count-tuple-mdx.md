---
title: Count (tupla) (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: COUNT
dev_langs: kbMDX
helpviewer_keywords: Count function [MDX]
ms.assetid: c8f4a570-54a8-4c00-ac4b-eef0ebdb353c
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: fedac649113ec0e062d3b9697bf46c0e006e20b3
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="count-tuple-mdx"></a>Count (Tupla) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o número de dimensões em uma tupla.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Tuple_Expression.Count  
```  
  
## <a name="arguments"></a>Argumentos  
 *Tuple_Expression*  
 Uma linguagem MDX válida que retorna uma tupla.  
  
## <a name="remarks"></a>Comentários  
 Retorna o número de dimensões em uma tupla.  
  
## <a name="example"></a>Exemplo  
 A medida calculada na consulta a seguir retorna o valor 2, que é o número de hierarquias presentes na tupla `([Measures].[Internet Sales Amount], [Date].[Calendar].[Calendar Year].&[2001])`:  
  
```  
WITH MEMBER MEASURES.COUNTTUPLE AS  
COUNT(([Measures].[Internet Sales Amount], [Date].[Calendar].[Calendar Year].&[2001]))  
SELECT MEASURES.COUNTTUPLE ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Contagem de &#40; dimensão &#41; &#40; MDX &#41;](../mdx/count-dimension-mdx.md)   
 [Contagem de &#40; Níveis de hierarquia &#41; &#40; MDX &#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Contagem de &#40; Definir &#41; &#40; MDX &#41;](../mdx/count-set-mdx.md)   
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
