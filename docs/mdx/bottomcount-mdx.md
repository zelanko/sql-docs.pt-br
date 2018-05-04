---
title: BottomCount (MDX) | Microsoft Docs
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
- BOTTOMCOUNT
dev_langs:
- kbMDX
helpviewer_keywords:
- BottomCount function
ms.assetid: 1441dab3-7885-4e92-9d48-21d832286677
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 4109e8241babdb49a53a233360092308b11c616b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="bottomcount-mdx"></a>BottomCount (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Remarks  
 Se for especificada uma expressão numérica, esta função classifica as tuplas no conjunto especificado de acordo com o valor da expressão numérica especificada conforme avaliada no conjunto, na ordem crescente. O **BottomCount** função retorna o número especificado de tuplas com o valor mais baixo.  
  
> [!IMPORTANT]  
>  O **BottomCount** função, como o [TopCount](../mdx/topcount-mdx.md) funcionar, sempre quebra a hierarquia.  
  
 Se uma expressão numérica não for especificada, a função retorna o conjunto de membros em ordem natural, sem qualquer classificação, se comportando como a [Tail (MDX)](../mdx/tail-mdx.md) função.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
