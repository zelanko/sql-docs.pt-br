---
title: Stdev (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a1ef1d720928298e8a44e075f45937903d178ef6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150248"
---
# <a name="stdev-mdx"></a>Stdev (MDX)


  Retorna o desvio padrão de exemplo de uma expressão numérica, avaliado em relação a um conjunto, usando a fórmula de população não polarizada (dividindo por n-1).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stdev(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Numeric_Expression*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número.  
  
## <a name="remarks"></a>Comentários  
 O **Stdev** função usa a população não polarizada fórmulas, enquanto o [StdevP](../mdx/stdevp-mdx.md) função usa a fórmula de população polarizada.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o desvio padrão para Quantidade de Pedidos pela Internet, avaliado em relação aos três primeiros meses do ano calendário 2003, usando a fórmula de população não polarizada.  
  
```  
WITH MEMBER Measures.x AS   
   Stdev   
   ( { [Date].[Calendar].[Month].[January 2003],  
       [Date].[Calendar].[Month].[February 2003],  
       [Date].[Calendar].[Month].[March 2003]},  
    [Measures].[Internet Order Quantity])  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
