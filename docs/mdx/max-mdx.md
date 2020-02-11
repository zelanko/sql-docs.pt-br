---
title: Max (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ad4bc2bf41caacbafb5bf36b5e95263ab2f85d22
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68098536"
---
# <a name="max-mdx"></a>Max (MDX)


  Retorna o valor máximo de uma expressão numérica que é avaliada sobre um conjunto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Max( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Numeric_Expression*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número.  
  
## <a name="remarks"></a>Comentários  
 Se uma expressão numérica for especificada, a expressão numérica especificada será avaliada pelo conjunto e então retornará o valor máximo daquela avaliação. Se uma expressão numérica não for especificada, o conjunto especificado será avaliado no contexto atual dos membros do conjunto e então retornará o valor máximo daquela avaliação.  
  
> [!NOTE]  
>  O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ignora nulos ao calcular o valor máximo em um conjunto de números.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna as vendas mensais máximas para cada trimestre, subcategoria e país no cubo Adventure Works.  
  
```  
WITH MEMBER Measures.x AS Max   
   ([Date].[Calendar].CurrentMember.Children  
      , [Measures].[Reseller Order Quantity]  
   )  
SELECT Measures.x ON 0  
,NON EMPTY [Date].[Calendar].[Calendar Quarter]*   
   [Product].[Product Categories].[Subcategory].members *  
   [Geography].[Geography].[Country].Members  
ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
