---
description: DistinctCount (MDX)
title: DistinctCount (MDX) | Microsoft Docs
ms.date: 11/12/2020
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 28807d1a24f97a6b197ad56d0434399ab53cd742
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584843"
---
# <a name="distinctcount-mdx"></a>DistinctCount (MDX)


  Retorna o número de tuplas distintas, não vazias em um conjunto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DistinctCount(Set_Expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
## <a name="remarks"></a>Comentários  
 A função **DistinctCount** é equivalente a `Count(Distinct(Set_Expression), EXCLUDEEMPTY)` .  
  
## <a name="examples"></a>Exemplos  
 A consulta a seguir mostra como usar a função DistinctCount:  
  
 `WITH SET MySet AS`  
  
 `{[Customer].[Customer Geography].[Country].&[Australia],[Customer].[Customer Geography].[Country].&[Australia],`  
  
 `[Customer].[Customer Geography].[Country].&[Canada],[Customer].[Customer Geography].[Country].&[France],`  
  
 `[Customer].[Customer Geography].[Country].&[United Kingdom],[Customer].[Customer Geography].[Country].&[United Kingdom]}`  
  
 `*`  
  
 `{([Date].[Calendar].[Date].&[20010701],[Measures].[Internet Sales Amount] )}`  
  
 `//Returns the value 3 because Internet Sales Amount is null`  
  
 `//for the UK on the date specified`  
  
 `MEMBER MEASURES.SETDISTINCTCOUNT AS`  
  
 `DISTINCTCOUNT(MySet)`  
  
 `SELECT {MEASURES.SETDISTINCTCOUNT} ON 0`  
  
 `FROM [Adventure Works]`  
 
A função DistinctCount retorna o número distinto de itens em um conjunto; Neste exemplo, o segundo parâmetro opcional é usado para excluir itens que não têm um valor para uma determinada tupla. Nesse caso, há quatro itens distintos no conjunto no primeiro parâmetro, mas a função retorna três porque apenas Austrália, Canadá e França têm dados de 1º de julho de 2001 para o valor de vendas pela Internet.
 
## <a name="see-also"></a>Consulte Também  
 [Contagem &#40;definida&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
