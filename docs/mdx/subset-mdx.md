---
title: Subconjunto (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e063d295480cff8e5db44f5ea30668a7a06ff74b
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581388"
---
# <a name="subset-mdx"></a>Subset (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna um subconjunto de tuplas de um conjunto especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Subset(Set_Expression, Start [ ,Count ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Iniciar*  
 Uma expressão numérica válida que especifica a posição da primeira tupla a ser retornada.  
  
 *Contagem*  
 Uma expressão numérica válida que especifica o número de tuplas a ser retornado.  
  
## <a name="remarks"></a>Remarks  
 Do conjunto especificado, o **subconjunto** função retorna um subconjunto que contém o número especificado de tuplas, começando na posição inicial especificada. A posição inicial baseia-se em um índice baseado em zero, isto é, zero (0) corresponde à primeira tupla no conjunto especificado, 1 corresponde à segunda e assim por diante.  
  
 Se *contagem* não for especificado, a função retornará todas as tuplas de *iniciar* até o final do conjunto.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna a medida Valor das Vendas do Revendedor para as cinco subcategorias principais de vendas dos produtos, independentemente da hierarquia, com base no Lucro Bruto do Revendedor. O **subconjunto** função é usada para retornar somente os primeiros cinco conjuntos no resultado após o resultado é ordenado com a **ordem** função.  
  
```  
SELECT Subset  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BDESC  
      )  
   ,0  
   ,5  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
