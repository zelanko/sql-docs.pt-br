---
description: Subset (MDX)
title: Subconjunto (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d0b7e79ebf0415011665ae63e7b9699200e374b1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386722"
---
# <a name="subset-mdx"></a>Subset (MDX)


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
  
 *Count*  
 Uma expressão numérica válida que especifica o número de tuplas a ser retornado.  
  
## <a name="remarks"></a>Comentários  
 A partir do conjunto especificado, a função **subconjunto** retorna um subconjunto que contém o número especificado de tuplas, começando na posição inicial especificada. A posição inicial baseia-se em um índice baseado em zero, isto é, zero (0) corresponde à primeira tupla no conjunto especificado, 1 corresponde à segunda e assim por diante.  
  
 Se *Count* não for especificado, a função retornará todas as tuplas do *início* ao fim do conjunto.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna a medida Valor das Vendas do Revendedor para as cinco subcategorias principais de vendas dos produtos, independentemente da hierarquia, com base no Lucro Bruto do Revendedor. A função **subconjunto** é usada para retornar apenas os cinco primeiros conjuntos no resultado depois que o resultado é ordenado usando a função **Order** .  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
