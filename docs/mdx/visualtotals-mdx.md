---
description: Função VisualTotals (MDX)
title: VisualTotals (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1c1e85f4384c322938f5e7937c32bcd116acdda2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500419"
---
# <a name="visualtotals-mdx"></a>Função VisualTotals (MDX)


  Retorna um conjunto gerado com a totalização dinâmica de membros filho em um conjunto especificado, utilizando, opcionalmente, um padrão para o nome do membro pai no conjunto de resultados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
VisualTotals(Set_Expression[,Pattern])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Padrão*  
 Uma expressão de cadeia de caracteres válida para o membro pai do conjunto, que contém um asterisco (*) como o caractere de substituição para o nome do pai.  
  
## <a name="remarks"></a>Comentários  
 A expressão de conjunto inserida pode especificar um conjunto que contém membros em qualquer nível de uma única dimensão, em geral, membros com uma relação ancestral-descendente. A função **VisualTotals** totaliza os valores dos membros filho no conjunto especificado e ignora os membros filho que não estão no conjunto no cálculo dos totais de resultado. Os totais são somados visualmente para conjuntos ordenados na ordem de hierarquia. Se a ordem de membros nos conjuntos quebrar a hierarquia, os resultados não serão totais visuais. Por exemplo, VisualTotals (EUA, WA, CA, Seattle) não retorna WA como Seattle, mas retorna os valores para WA, CA e Seattle e, em seguida, soma esses valores como o total visual para os EUA, contando as vendas de Seattle duas vezes.  
  
> [!NOTE]  
>  Aplicar a função **VisualTotals** a membros de dimensão que não estão relacionados a uma medida ou que estão sob a granularidade do grupo de medidas fará com que os valores sejam substituídos por um valor nulo.  
  
 *Padrão*, que é opcional, especifica o formato do rótulo de totais. O *padrão* requer um asterisco (*), pois o caractere de substituição para o membro pai e o restante do texto na cadeia de caracteres aparecem no resultado concatenado com o nome pai. Para exibir um asterisco literal, use dois asteriscos ( \* \* ).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o total visual do terceiro trimestre do ano civil de 2001 com base no único descendente especificado, o mês de julho.  
  
```  
SELECT VisualTotals  
   ({[Date].[Calendar].[Calendar Quarter].&[2001]&[3]  
      ,[Date].[Calendar].[Month].&[2001]&[7]}) ON 0  
FROM [Adventure Works]  
```  
  
 O exemplo a seguir retorna o membro [All] da hierarquia de atributo Categoria na dimensão Produto junto com dois dos quatro filhos. O total retornado para o membro [All] para a medida Valor de Vendas da Intenet é o total apenas dos membros Acessórios e Roupas. Além disso, o argumento do padrão é usado para especificar o rótulo da coluna [All Products].  
  
```  
SELECT  
   VisualTotals  
   ({[Product].[Category].[All Products]  
      ,[Product].[Category].[Accessories]  
      ,[Product].[Category].[Clothing]}  
      , '* - Visual Total'  
   ) ON Columns  
, [Measures].[Internet Sales Amount] ON Rows  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
