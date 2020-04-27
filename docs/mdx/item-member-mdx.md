---
title: Item (membro) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d7afa88f9d6239c8da7cb9c406ef11f0764f8dcf
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67905915"
---
# <a name="item-member-mdx"></a>Item (Membro) (MDX)


  Retorna um membro de uma tupla especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Tuple_Expression.Item( Index )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Tuple_Expression*  
 Uma linguagem MDX válida que retorna uma tupla.  
  
 *Índice*  
 Uma expressão numérica válida que especifica o membro específico através da posição dentro da tupla a ser retornada.  
  
## <a name="remarks"></a>Comentários  
 A função **Item** retorna um membro da tupla especificada. A função retorna o membro encontrado na posição baseada em zero especificada pelo *índice*.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o membro `[2003]` - o primeiro item na tupla `[Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).` - nas colunas :  
  
 `SELECT`  
  
 `{( [Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).Item(0)} ON 0`  
  
 `,{[Measures].[Reseller Sales Amount]} ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
