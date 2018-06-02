---
title: Tail (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5192deedcb6085767fc00f68bb17f6adddb38679
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581238"
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
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
