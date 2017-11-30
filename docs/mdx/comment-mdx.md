---
title: "Comentário (MDX) | Microsoft Docs"
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
f1_keywords:
- '*/'
- /*
dev_langs: kbMDX
helpviewer_keywords:
- commenting characters
- /*...*/ (comment)
ms.assetid: 64434ae4-80ce-4634-86b8-4125dfaa7f61
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: f09911224fb93b1ba5ca70ecf57d933f67f3f85b
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="comment-mdx"></a>Comentário (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Indica o texto de comentário fornecido pelo usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
/* Comment_Text */      
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Comment_Text*  
 Cadeia de caracteres que contém o texto do comentário.  
  
## <a name="remarks"></a>Comentários  
 O servidor não avalia o texto entre os caracteres de comentário / * e \*/. Eles podem ser inseridos em uma linha separada ou dentro de uma instrução MDX. Comentários de várias linhas devem ser indicados por /\* e \*/.  
  
 Não há comprimento máximo para comentários. Os comentários podem ser aninhados; por exemplo, `/* Test /*Comment*/ Text*/` é um exemplo de um comentário aninhado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir demonstra o uso desse operador.  
  
```  
/* This member returns the gross profit margin for product types  
  and reseller types crossjoined by year. */  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
    [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM /* Select from the Adventure Works cube. */  
    [Adventure Works]  
WHERE  
    [Measures].[Gross Profit Margin]  
```  
  
## <a name="see-also"></a>Consulte também  
 [&#40; Comentário &#41; &#40; MDX &#41;](../mdx/comment-mdx-double-slash.md)   
 [– &#40; Comentário &#41; &#40; MDX &#41;](../mdx/comment-mdx-operator-reference.md)   
 [Referência de operador MDX &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
