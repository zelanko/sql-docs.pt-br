---
title: UniqueName (MDX) | Microsoft Docs
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
f1_keywords: UNIQUENAME
dev_langs: kbMDX
helpviewer_keywords: UniqueName function
ms.assetid: f186094e-670c-401c-a82f-6b634b3f71f5
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 1371b4e28fb7380f250fb1eab9630c5c24b52c87
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="uniquename-mdx"></a>UniqueName (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o nome exclusivo de uma dimensão, hierarquia, nível ou membro especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Dimension expression syntax  
Dimension_Expression.UniqueName  
  
Hierarchy expression syntax  
Hierarchy_Expression.UniqueName  
  
Level expression syntax  
Level_Expression.UniqueName  
  
Member expression syntax  
Member_Expression.UniqueName  
```  
  
## <a name="arguments"></a>Argumentos  
 *Dimension_Expression*  
 Uma linguagem MDX válida que retorna uma expressão que será resolvida em uma dimensão.  
  
 *Expressão_Hierarquia*  
 Uma linguagem MDX válida que retorna uma hierarquia.  
  
 *Level_Expression*  
 Uma linguagem MDX válida que retorna um nível.  
  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Comentários  
 O **UniqueName** função retorna o nome exclusivo do objeto, não o nome retornado pelo [nome](../mdx/name-mdx.md) função. O nome retornado não inclui o nome do cubo. Os resultados retornados dependem das configurações do servidor ou da propriedade de cadeia de conexão MDX Unique Name Style.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna um valor de nome exclusivo para a dimensão Produto, a hierarquia Categorias de Produtos, nível Subcategoria e o membro Suportes para Bicicleta do cubo Adventure Works.  
  
```  
WITH MEMBER DimensionUniqueName   
   AS [Product].UniqueName  
MEMBER HierarchyUniqueName   
   AS [Product].[Product Categories].UniqueName  
MEMBER LevelUniqueName   
   AS [Product].[Product Categories].[Subcategory].UniqueName  
MEMBER MemberUniqueName   
   AS [Product].[Product Categories].[Subcategory].[Bike Racks]  
SELECT   
   {DimensionUniqueName  
   , HierarchyUniqueName  
   , LevelUniqueName  
   , MemberUniqueName }  
   ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
