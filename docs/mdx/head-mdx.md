---
title: Head (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6e6d8da7a5813f7e99c022e19f18de2800598885
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
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
 O **Head** função retorna o número especificado de tuplas desde o início do conjunto especificado. A ordem dos elementos é preservada. O valor padrão de Count é 1. Se o número especificado de tuplas for menor que 1, o **Head** função retorna um conjunto vazio. Se o número especificado de tuplas ultrapassar o número de tuplas no conjunto, a função retornará o conjunto original.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna as cinco subcategorias principais de vendas dos produtos, independentemente da hierarquia, com base no Lucro Bruto do Revendedor. O **Head** função é usada para retornar somente os 5 primeiros conjuntos no resultado, após o resultado é ordenado com o **ordem** função.  
  
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
 [Parte final &#40;MDX&#41;](../mdx/tail-mdx.md)   
 [Item &#40;tupla&#41; &#40;MDX&#41;](../mdx/item-tuple-mdx.md)   
 [Item &#40;membro&#41; &#40;MDX&#41;](../mdx/item-member-mdx.md)   
 [Classificação &#40;MDX&#41;](../mdx/rank-mdx.md)   
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
