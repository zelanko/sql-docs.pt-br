---
title: Members (conjunto) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3bd4fe92c064f4665a4b397e47a45ae5bde50f39
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63048440"
---
# <a name="members-set-mdx"></a>Members (Conjunto) (MDX)


  Retorna o conjunto de membros em uma dimensão, nível ou hierarquia.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Hierarchy expression syntax  
Hierarchy_Expression.Members  
  
Level expression Syntax  
Level_Expression.Members  
```  
  
## <a name="arguments"></a>Argumentos  
 *Hierarchy_Expression*  
 Uma linguagem MDX válida que retorna uma hierarquia.  
  
 *Level_Expression*  
 Uma linguagem MDX válida que retorna um nível.  
  
## <a name="remarks"></a>Comentários  
 Se uma expressão de hierarquia for especificada, o **Members (conjunto)** função retorna o conjunto de todos os membros dentro da hierarquia especificada, não incluindo os membros calculados. Para obter o conjunto de todos os membros, calculados ou caso contrário, em uma hierarquia, use o [AllMembers &#40;MDX&#41; ](../mdx/allmembers-mdx.md) função  
  
 Se uma expressão de nível for especificada, o **Members (conjunto)** função retorna o conjunto de todos os membros dentro do nível especificado.  
  
> [!IMPORTANT]  
>  Quando uma dimensão contém apenas uma única hierarquia visível, a hierarquia pode ser mencionada pelo nome da dimensão ou pelo nome da hierarquia porque o nome da dimensão, neste cenário, é resolvido apenas na hierarquia visível. Por exemplo, Measures.Members é uma expressão MDX válida porque é resolvida na única hierarquia da dimensão Measures.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o conjunto de todos os membros da hierarquia Ano Civil no cubo Adventure Works.  
  
```  
SELECT   
   [Date].[Calendar].[Calendar Year].Members ON 0  
FROM  
   [Adventure Works]  
  
```  
  
 O exemplo a seguir retorna a quantidade de pedidos de 2003 para cada membro no nível `[Product].[Products].[Product Line]`. O **membros** função retorna um conjunto que representa todos os membros no nível.  
  
```  
SELECT   
   {Measures.[Order Quantity]} ON COLUMNS,  
   [Product].[Product Line].[Product Line].Members ON ROWS  
FROM  
   [Adventure Works]  
WHERE  
   {[Date].[Calendar Year].[Calendar Year].&[2003]}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
