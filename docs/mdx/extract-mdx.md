---
description: Extract (MDX)
title: Extrair (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0b168794a38a515d4ace97d576710041eac86195
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387512"
---
# <a name="extract-mdx"></a>Extract (MDX)


  Retorna um conjunto de tuplas dos elementos de hierarquia extraídos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Extract(Set_Expression, Hierarchy_Expression1 [,Hierarchy_Expression2, ...n] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Hierarchy_Expression1*  
 Uma linguagem MDX válida que retorna uma hierarquia.  
  
 *Hierarchy_Expression2*  
 Uma linguagem MDX válida que retorna uma hierarquia.  
  
## <a name="remarks"></a>Comentários  
 A função **Extract** retorna um conjunto que consiste em tuplas dos elementos de hierarquia extraídos. Para cada tupla no conjunto especificado, os membros das hierarquias especificadas são extraídos em novas tuplas no conjunto de resultados. Esta função sempre remove tuplas duplicadas.  
  
 A função **Extract** executa a ação oposta da função de [interjunção](../mdx/crossjoin-mdx.md) .  
  
## <a name="examples"></a>Exemplos  
 A consulta a seguir mostra como usar a função **Extract** em um conjunto de tuplas retornado pela função não **vazia** :  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `//Returns the distinct combinations of Customer and Date for all purchases`  
  
 `//of Bike Racks or Bike Stands`  
  
 `EXTRACT(`  
  
 `NONEMPTY(`  
  
 `[Customer].[Customer].[Customer].MEMBERS`  
  
 `*`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `*`  
  
 `{[Product].[Product Categories].[Subcategory].&[26],[Product].[Product Categories].[Subcategory].&[27]}`  
  
 `*`  
  
 `{[Measures].[Internet Sales Amount]}`  
  
 `)`  
  
 `,  [Customer].[Customer], [Date].[Date])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
