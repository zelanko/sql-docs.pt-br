---
title: Subconjunto (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: subset
dev_langs: kbMDX
helpviewer_keywords: Subset function
ms.assetid: 49a7cd28-cd6f-4ae7-8c91-94a8652a97a5
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 86014760cec4a433b43c93e8e2186b8018cf49da
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="subset-mdx"></a>Subset (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="remarks"></a>Comentários  
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
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
