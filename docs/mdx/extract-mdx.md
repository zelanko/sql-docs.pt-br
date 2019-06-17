---
title: Extrair (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a3c58799cc3e95efd7d49b3aff0bf31a1fce22b1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63155212"
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
 O **extrair** função retorna um conjunto que consiste em tuplas de elementos de hierarquia extraídos. Para cada tupla no conjunto especificado, os membros das hierarquias especificadas são extraídos em novas tuplas no conjunto de resultados. Esta função sempre remove tuplas duplicadas.  
  
 O **extrair** função executa a ação oposta das [Crossjoin](../mdx/crossjoin-mdx.md) função.  
  
## <a name="examples"></a>Exemplos  
 A consulta a seguir mostra como usar o **extrair** função em um conjunto de tuplas retornado pela **NonEmpty** função:  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
