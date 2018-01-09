---
title: Extrair (MDX) | Microsoft Docs
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
f1_keywords: EXTRACT
dev_langs: kbMDX
helpviewer_keywords: Extract function
ms.assetid: c0d27d31-e36e-4b7f-bb86-1e4707351392
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 4a92701862d0cfcf3881c493c7e062c73fbd9aa6
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="extract-mdx"></a>Extract (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Remarks  
 O **extrair** função retorna um conjunto composto de tuplas dos elementos da hierarquia extraídos. Para cada tupla no conjunto especificado, os membros das hierarquias especificadas são extraídos em novas tuplas no conjunto de resultados. Esta função sempre remove tuplas duplicadas.  
  
 O **extrair** função executa a ação oposta do [Crossjoin](../mdx/crossjoin-mdx.md) função.  
  
## <a name="examples"></a>Exemplos  
 A consulta a seguir mostra como usar o **extrair** função em um conjunto de tuplas retornado pelo **NonEmpty** função:  
  
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
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
