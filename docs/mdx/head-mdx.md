---
title: Cabeçalho (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6e6d8da7a5813f7e99c022e19f18de2800598885
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67906005"
---
# <a name="head-mdx"></a>Head (MDX)


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
  
## <a name="remarks"></a>Comentários  
 A função **Head** retorna o número especificado de tuplas desde o início do conjunto especificado. A ordem dos elementos é preservada. O valor padrão de Count é 1. Se o número especificado de tuplas for menor que 1, a função **Head** retornará um conjunto vazio. Se o número especificado de tuplas ultrapassar o número de tuplas no conjunto, a função retornará o conjunto original.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna as cinco subcategorias principais de vendas dos produtos, independentemente da hierarquia, com base no Lucro Bruto do Revendedor. A função **Head** é usada para retornar apenas os cinco primeiros conjuntos no resultado depois que o resultado é ordenado usando a função **Order** .  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [&#40;&#41;da parte final do MDX](../mdx/tail-mdx.md)   
 [&#40;de tupla de item&#41; &#40;MDX&#41;](../mdx/item-tuple-mdx.md)   
 [Membro de &#40;de item&#41; &#40;MDX&#41;](../mdx/item-member-mdx.md)   
 [Classificação &#40;&#41;MDX](../mdx/rank-mdx.md)   
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
