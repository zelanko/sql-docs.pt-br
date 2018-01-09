---
title: Tail (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: TAIL
dev_langs: kbMDX
helpviewer_keywords: Tail function
ms.assetid: d62a1bb2-55c0-4939-8526-cdc3d444ffe2
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 2d8781dc0364699146d1d3706a8e2e976acc1f7c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="tail-mdx"></a>Tail (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna um subconjunto desde o final de um conjunto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Tail(Set_Expression [ ,Count ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Contagem*  
 Uma expressão numérica válida que especifica o número de tuplas a ser retornado.  
  
## <a name="remarks"></a>Remarks  
 O **final** função retorna o número especificado de tuplas do final do conjunto especificado. A ordem dos elementos é preservada. O valor padrão de *contagem* é 1. Se o número especificado de tuplas for inferior a 1, a função retornará um conjunto vazio. Se o número especificado de tuplas ultrapassar o número de tuplas no conjunto, a função retornará o conjunto original.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna a medida Valor das Vendas do Revendedor para as cinco subcategorias principais de vendas dos produtos, independentemente da hierarquia, com base no Lucro Bruto do Revendedor. O **final** função é usada para retornar apenas os últimos cinco conjuntos no resultado, depois do resultado é ordenado inversamente usando o **ordem** função.  
  
```  
SELECT Tail  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BASC  
      )  
   ,5  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
