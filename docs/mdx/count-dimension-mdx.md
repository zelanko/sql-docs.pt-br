---
title: "Count (dimensão) (MDX) | Microsoft Docs"
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
f1_keywords: COUNT
dev_langs: kbMDX
helpviewer_keywords: Count function [MDX]
ms.assetid: 4b9c52f6-5bb0-401a-947c-e14134558b4a
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 7c75e556f86ad2c433e97e44474048e042603861
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="count-dimension-mdx"></a>Count (Dimensão) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o número de hierarquias em um cubo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Dimensions.Count   
```  
  
## <a name="remarks"></a>Remarks  
 Retorna o número de hierarquias em um cubo, inclusive a hierarquia `[Measures].[Measures]`.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o número de hierarquias no cubo Adventure Works.  
  
```  
WITH MEMBER measures.X AS  
  dimensions.count   
SELECT Measures.X ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Contagem de &#40; Coleção de itens &#41; &#40; MDX &#41;](../mdx/count-tuple-mdx.md)   
 [Contagem de &#40; Níveis de hierarquia &#41; &#40; MDX &#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Contagem de &#40; Definir &#41; &#40; MDX &#41;](../mdx/count-set-mdx.md)   
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
