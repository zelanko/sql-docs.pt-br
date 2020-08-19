---
description: DrillupLevel (MDX)
title: DrillupLevel (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cfdb8e77fcb92fe208e83f45c32a5c20c5d29615
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421900"
---
# <a name="drilluplevel-mdx"></a>DrillupLevel (MDX)


  Faz drill up dos membros de um conjunto que estão abaixo de um nível especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DrillupLevel(Set_Expression [ , Level_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Level_Expression*  
 Uma linguagem MDX válida que retorna um nível.  
  
## <a name="remarks"></a>Comentários  
 A função **DrillupLevel** retorna um conjunto de membros organizados hierarquicamente com base nos membros incluídos no conjunto especificado. A ordem é preservada entre os membros do conjunto especificado.  
  
 Se uma expressão de nível for especificada, a função **DrillupLevel** construirá o conjunto recuperando somente os membros que estão acima do nível especificado. Se uma expressão de nível for especificada e não houver nenhum membro do nível especificado representado no conjunto especificado, esse conjunto será retornado.  
  
 Se uma expressão de nível não for especificada, a função construirá o conjunto, recuperando apenas aqueles membros que estão um nível acima do nível mais baixo da primeira dimensão referenciada no conjunto especificado.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o conjunto de membros do primeiro conjunto que estão acima do nível Subcategoria.  
  
```  
SELECT DrillUpLevel   
  ({[Product].[Product Categories].[All Products]  
    ,[Product].[Product Categories].[Subcategory].&[32],  
    [Product].[Product Categories].[Product].&[215]},  
  [Product].[Product Categories].[Subcategory]  
    )  
  ON 0  
  FROM [Adventure Works]  
  WHERE [Measures].[Internet Order Quantity]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
