---
title: Head (MDX) | Microsoft Docs
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
- HEAD
dev_langs:
- kbMDX
helpviewer_keywords:
- Head function
ms.assetid: 2a909bda-1366-4537-93b0-c089554fc11f
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 5529333ef2e81b8fee7d78765e0fb528ecb02577
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="head-mdx"></a>Head (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o primeiro número especificado de elementos em um conjunto, mantendo as duplicatas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Head(Set_Expression [ ,Count ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Count*  
 Uma expressão numérica válida que especifica o número de tuplas a ser retornado.  
  
## <a name="remarks"></a>Remarks  
 O **Head** função retorna o número especificado de tuplas desde o início do conjunto especificado. A ordem dos elementos é preservada. O valor padrão de Count é 1. Se o número especificado de tuplas for menor que 1, o **Head** função retorna um conjunto vazio. Se o número especificado de tuplas ultrapassar o número de tuplas no conjunto, a função retornará o conjunto original.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna as cinco subcategorias principais de vendas dos produtos, independentemente da hierarquia, com base no Lucro Bruto do Revendedor. O **Head** função é usada para retornar somente os 5 primeiros conjuntos no resultado, após o resultado é ordenado com a **ordem** função.  
  
```  
SELECT   
[Measures].[Reseller Gross Profit] ON 0,  
Head  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BDESC  
      )  
   ,5  
   ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Final &#40;MDX&#41;](../mdx/tail-mdx.md)   
 [Item &#40;tupla&#41; &#40;MDX&#41;](../mdx/item-tuple-mdx.md)   
 [Item &#40;membro&#41; &#40;MDX&#41;](../mdx/item-member-mdx.md)   
 [Classificação &#40;MDX&#41;](../mdx/rank-mdx.md)   
 [Referência de função MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
