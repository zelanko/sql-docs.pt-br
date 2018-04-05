---
title: Count (níveis de hierarquia) (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- COUNT
dev_langs:
- kbMDX
helpviewer_keywords:
- Count function [MDX]
ms.assetid: 3de6a824-2ff3-47ac-9ceb-e3369a04f35d
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: b68bb6f266fefff1274241e6f5b2860fb522fb02
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="count-hierarchy-levels-mdx"></a>Count (Níveis de hierarquia) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o número de níveis na hierarquia.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Hierarchy_Expression.Levels.Count  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expressão_Hierarquia*  
 Uma linguagem MDX válida que retorna uma hierarquia.  
  
## <a name="remarks"></a>Remarks  
 Retorna o número de níveis em uma hierarquia, incluindo o nível `[All]`, se aplicável.  
  
> [!IMPORTANT]  
>  Quando uma dimensão contém apenas uma única hierarquia visível, a hierarquia pode ser mencionada pelo nome da dimensão ou pelo nome da hierarquia porque o nome da dimensão é resolvido apenas na hierarquia visível. Por exemplo, `Measures.Levels.Count` é uma expressão MDX válida porque é resolvida na única hierarquia da dimensão Measures.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna uma contagem do número de níveis na hierarquia Categorias de Produtos definida pelo usuário no cubo Adventure Works.  
  
```  
WITH MEMBER measures.X AS  
   [Product].[Product Categories].Levels.Count   
Select Measures.X ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Contagem de &#40; dimensão &#41; &#40; MDX &#41;](../mdx/count-dimension-mdx.md)   
 [Contagem de &#40; Coleção de itens &#41; &#40; MDX &#41;](../mdx/count-tuple-mdx.md)   
 [Contagem de &#40; Definir &#41; &#40; MDX &#41;](../mdx/count-set-mdx.md)   
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
