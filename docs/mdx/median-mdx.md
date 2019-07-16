---
title: Mediana (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b6f941e269bb9948dd39ba52db0ea4d0961c029a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033848"
---
# <a name="median-mdx"></a>Median (MDX)


  Retorna o valor mediano de uma expressão numérica que é avaliada sobre um conjunto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Median(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Numeric_Expression*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número.  
  
## <a name="remarks"></a>Comentários  
 Se uma expressão numérica for especificada, essa expressão será avaliada pelo conjunto e, depois, retornará o valor mediano da avaliação em questão. Se uma expressão numérica não for especificada, o conjunto especificado será avaliado no contexto atual dos membros do conjunto e retornará o valor mediano daquela avaliação.  
  
 O valor mediano é o valor médio em um conjunto de números ordenados. (O valor mediano é diferente do valor médio, que é a soma de um conjunto de números dividida pela contagem de números no conjunto). O valor mediano é determinado escolhendo-se o valor menor de maneira que pelo menos a metade dos valores no conjunto não sejam maiores do que o valor escolhido. Se o número de valores dentro do conjunto for ímpar, o valor mediano corresponderá a um valor único. Se o número de valores dentro do conjunto for par, o valor mediano corresponderá à soma dos dois valores do meio dividido por dois.  
  
> [!NOTE]  
>  O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ignora nulos ao calcular o valor mediano em um conjunto de números ordenados.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna as vendas mensais medianas para cada trimestre, cada subcategoria e cada país no cubo Adventure Works.  
  
```  
WITH MEMBER Measures.x AS Median   
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
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
