---
description: BottomCount (MDX)
title: BottomCount (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e331a84efe36cef11951afac3f304957e4ffcb00
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494970"
---
# <a name="bottomcount-mdx"></a>BottomCount (MDX)


  Classifica um conjunto na ordem crescente e retorna o número especificado de tuplas no conjunto especificado com os valores mais baixos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BottomCount(Set_Expression, Count [,Numeric_Expression])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Count*  
 Uma expressão numérica válida que especifica o número de tuplas a ser retornado.  
  
 *Numeric_Expression*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número.  
  
## <a name="remarks"></a>Comentários  
 Se for especificada uma expressão numérica, esta função classifica as tuplas no conjunto especificado de acordo com o valor da expressão numérica especificada conforme avaliada no conjunto, na ordem crescente. A função **BottomCount** retorna o número especificado de tuplas com o menor valor.  
  
> [!IMPORTANT]  
>  A função **BottomCount** , como a função [TopCount](../mdx/topcount-mdx.md) , sempre interrompe a hierarquia.  
  
 Se uma expressão numérica não for especificada, a função retornará o conjunto de membros em ordem natural, sem nenhuma classificação, comportando-se como a função [final (MDX)](../mdx/tail-mdx.md) .  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna a medida Quantidade de Pedidos do Revendedor para cada ano calendário para as cinco vendas inferiores em subcategorias de produtos, classificadas com base na medida Valor das Vendas do Revendedor.  
  
```  
SELECT BottomCount([Product].[Product Categories].[Subcategory].Members  
   , 10  
   , [Measures].[Reseller Sales Amount]) ON 0,  
   [Date].[Calendar].[Calendar Year].Members ON 1  
  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Reseller Order Quantity]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
