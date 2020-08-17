---
description: Comentário (MDX)
title: Comentário (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0a06660c0e542f789caa4f4df353559cced4537f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387682"
---
# <a name="comment-mdx"></a>Comentário (MDX)


  Indica o texto de comentário fornecido pelo usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
/* Comment_Text */      
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Comment_Text*  
 Cadeia de caracteres que contém o texto do comentário.  
  
## <a name="remarks"></a>Comentários  
 O servidor não avalia o texto entre os caracteres de comentário,/* e \* /. Eles podem ser inseridos em uma linha separada ou dentro de uma instrução MDX. Comentários de várias linhas devem ser indicados por/ \* e \* /.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [ Comentário de&#40;&#41; &#40;MDX&#41;](../mdx/comment-mdx-double-slash.md)   
 [-- &#40;Comment&#41; &#40;MDX&#41;](../mdx/comment-mdx-operator-reference.md)   
 [Referência de operador MDX &#40;&#41;MDX ](../mdx/mdx-operator-reference-mdx.md)  
  
  
