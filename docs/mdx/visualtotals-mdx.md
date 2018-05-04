---
title: VisualTotals (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- VisualTotals
dev_langs:
- kbMDX
helpviewer_keywords:
- VisualTotals function
ms.assetid: 8ec529c2-729a-4a5b-892e-750849ab4013
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 0cb3e14d9eb45f0354e0196a4861333a95630d4e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="visualtotals-mdx"></a>Função VisualTotals (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Remarks  
 A expressão de conjunto inserida pode especificar um conjunto que contém membros em qualquer nível de uma única dimensão, em geral, membros com uma relação ancestral-descendente. O **VisualTotals** função totalize os valores dos membros filho no conjunto especificado e ignora os membros filho que não estão no conjunto ao calcular os totais de resultado. Os totais são somados visualmente para conjuntos ordenados na ordem de hierarquia. Se a ordem de membros nos conjuntos quebrar a hierarquia, os resultados não serão totais visuais. Por exemplo, VisualTotals (EUA, WA, CA, Seattle) não retorna WA como Seattle, mas retorna os valores para WA, CA e Seattle e, em seguida, soma esses valores como o total visual para os EUA, contando as vendas de Seattle duas vezes.  
  
> [!NOTE]  
>  Aplicar o **VisualTotals** função para membros de dimensão que não estão relacionadas a uma medida ou estão sob a granularidade do grupo de medidas fará com que valores nulos.  
  
 *Padrão de*, que é opcional, especifica o formato do rótulo de totais. *Padrão* requer um asterisco (*) como o caractere de substituição para o membro pai e o restante do texto na cadeia de caracteres aparece no resultado concatenado com o nome do pai. Para exibir um asterisco literal, use dois asteriscos (\*\*).  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
