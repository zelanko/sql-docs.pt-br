---
title: (Comentário) (MDX) | Microsoft Docs
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
- //
dev_langs:
- kbMDX
helpviewer_keywords:
- commenting characters
- // (comment)
ms.assetid: 9a3ee822-4689-41a8-9997-8b307850cd68
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: ad8cdbf46838883892ce6e65a14d5bff78ff496b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="comment-mdx-double-slash"></a>Barras duplas de MDX de comentário
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Indica texto fornecido pelo usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
// Comment_Text   
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Comment_Text*  
 Cadeia de caracteres que contém o texto do comentário.  
  
## <a name="remarks"></a>Remarks  
 Os comentários podem ser inseridos em uma linha separada, aninhados no final de uma linha de script MDX ou aninhados em uma instrução MDX. O servidor não avalia o comentário.  
  
 Use // somente para comentários de linha única. Os comentários inseridos com // são delimitados pelo caractere de nova linha.  
  
 Não há comprimento máximo para comentários.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir demonstra o uso desse operador.  
  
```  
// This member returns the gross profit margin for product types  
// and reseller types crossjoined by year.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
      [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM // Select from the Adventure Works cube.  
    [Adventure Works]  
WHERE  
    [Measures].[Gross Profit Margin]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Comentário & #40; MDX & #41;](../mdx/comment-mdx.md)   
 [– & #40; Comentário & #41; & #40; MDX & #41;](../mdx/comment-mdx-operator-reference.md)   
 [Referência de operador MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
