---
title: Item (membro) (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ITEM
dev_langs:
- kbMDX
helpviewer_keywords:
- Item function
ms.assetid: 71cca249-910b-4ecd-9097-1a17b224e219
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4c2649598e6224c3458dfa0b0278df8d6458b7ce
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="item-member-mdx"></a>Item (Membro) (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 O **Item** função retorna um membro da tupla especificada. A função retorna o membro encontrado na posição de base zero especificada por *índice*.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o membro `[2003]` - o primeiro item na tupla `[Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).` - nas colunas :  
  
 `SELECT`  
  
 `{( [Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).Item(0)} ON 0`  
  
 `,{[Measures].[Reseller Sales Amount]} ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

