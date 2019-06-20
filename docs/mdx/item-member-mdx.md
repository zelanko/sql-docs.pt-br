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
manager: kfile
ms.openlocfilehash: 92745085a408503a2b435eb160daf431c7fdaa32
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63272838"
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
  
 *Index*  
 Uma expressão numérica válida que especifica o membro específico através da posição dentro da tupla a ser retornada.  
  
## <a name="remarks"></a>Comentários  
 O **Item** função retorna um membro da tupla especificada. A função retorna o membro encontrado na posição baseada em zero especificada por *índice*.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o membro `[2003]` - o primeiro item na tupla `[Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).` - nas colunas :  
  
 `SELECT`  
  
 `{( [Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).Item(0)} ON 0`  
  
 `,{[Measures].[Reseller Sales Amount]} ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
