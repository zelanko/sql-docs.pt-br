---
title: Min (MDX) | Microsoft Docs
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
f1_keywords: MIN
dev_langs: kbMDX
helpviewer_keywords: Min function [MDX]
ms.assetid: 9f3799c0-2502-4056-a259-053898f69b7c
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 013448ce1f7b234866a514a42653c3ffe98008a6
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="min-mdx"></a>Min (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o valor mínimo de uma expressão numérica que é avaliada sobre um conjunto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Min( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Numeric_Expression*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número.  
  
## <a name="remarks"></a>Remarks  
 Se uma expressão numérica for especificada, essa expressão será avaliada pelo conjunto e retornará o valor mínimo da avaliação em questão. Se uma expressão numérica não for especificada, o conjunto especificado será avaliado no contexto atual dos membros do conjunto e retornarão o valor mínimo daquela avaliação.  
  
> [!NOTE]  
>  O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ignora nulos ao calcular o valor mínimo em um conjunto de números.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna as vendas trimestrais mínimas para cada subcategoria e cada país no cubo Adventure Works.  
  
```  
WITH MEMBER Measures.x AS Min   
   ([Date].[Calendar].CurrentMember.Children  
      , [Measures].[Reseller Order Quantity]  
   )  
SELECT Measures.x ON 0  
,NON EMPTY [Date].[Calendar].[Calendar Quarter]*   
   [Product].[Product Categories].[Subcategory].members *  
   [Geography].[Geography].[Country].Members  
ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
