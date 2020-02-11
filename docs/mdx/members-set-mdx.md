---
title: Membros (conjunto) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d3e5bb14455d2d2ea67c4187e8e1a2a420031944
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138262"
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
 Se uma expressão de hierarquia for especificada, a função **Members (Set)** retornará o conjunto de todos os membros dentro da hierarquia especificada, não incluindo os membros calculados. Para obter o conjunto de todos os membros, calculados ou de outra forma, em uma hierarquia, use a função [&#40;MDX&#41;](../mdx/allmembers-mdx.md)  
  
 Se uma expressão de nível for especificada, a função **Members (Set)** retornará o conjunto de todos os membros dentro do nível especificado.  
  
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
  
 O exemplo a seguir retorna a quantidade de pedidos de 2003 para cada membro no nível `[Product].[Products].[Product Line]`. A função **Members** retorna um conjunto que representa todos os membros no nível.  
  
```  
SELECT   
   {Measures.[Order Quantity]} ON COLUMNS,  
   [Product].[Product Line].[Product Line].Members ON ROWS  
FROM  
   [Adventure Works]  
WHERE  
   {[Date].[Calendar Year].[Calendar Year].&[2003]}  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)   
 [Referência de função MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
