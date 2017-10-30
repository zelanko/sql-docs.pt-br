---
title: DrillupLevel (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DRILLUPLEVEL
dev_langs:
- kbMDX
helpviewer_keywords:
- DrillupLevel function
ms.assetid: 63431f79-f3a1-40c4-bf57-2b6bd8991cc3
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a59de1459ecc5953b4612c64603eff958049e3e6
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="drilluplevel-mdx"></a>DrillupLevel (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 O **DrillupLevel** função retorna um conjunto de membros organizado hierarquicamente com base nos membros incluídos no conjunto especificado. A ordem é preservada entre os membros do conjunto especificado.  
  
 Se uma expressão de nível for especificada, o **DrillupLevel** função constrói o conjunto, recuperando apenas aqueles membros que estão acima do nível especificado. Se uma expressão de nível for especificada e não houver nenhum membro do nível especificado representado no conjunto especificado, esse conjunto será retornado.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

