---
title: Trabalhando com membros, tuplas e conjuntos (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MDX [Analysis Services], tuples
- member keys [MDX]
- MDX [Analysis Services], sets
- calculated members [MDX]
- members [MDX]
- Multidimensional Expressions [Analysis Services], members
- named sets [MDX]
- Multidimensional Expressions [Analysis Services], tuples
- member functions [MDX]
- sets [MDX]
- MDX [Analysis Services], members
- member names [MDX]
- Multidimensional Expressions [Analysis Services], sets
- tuple functions
- tuples
- set functions [MDX]
ms.assetid: b6ec2439-caef-46d3-9fd7-5f4526cee334
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c5929d1c9d926005cd919d4e939e46c950723b64
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="working-with-members-tuples-and-sets-mdx"></a>Trabalhando com membros, tuplas e conjuntos (MDX)
  A linguagem MDX fornece inúmeras funções que retornam um ou mais membros, tuplas ou conjuntos ou que agem como tais.  
  
## <a name="member-functions"></a>Funções de membro  
 A linguagem MDX fornece várias funções para recuperar membros de outras entidades MDX, como de dimensões, níveis, conjuntos ou tuplas. Por exemplo, a função [FirstChild](../../../mdx/firstchild-mdx.md) é uma função que age em um membro e retorna um membro.  
  
 Para obter o primeiro membro filho da dimensão Tempo, você pode declarar explicitamente o membro, como no exemplo a seguir.  
  
```  
SELECT [Date].[Calendar Year].[CY 2001] on 0  
FROM [Adventure Works]  
  
```  
  
 Também é possível usar a função **FirstChild** para retornar o mesmo membro, como no exemplo a seguir.  
  
```  
SELECT [Date].[Calendar Year].FirstChild on 0  
FROM [Adventure Works]  
  
```  
  
 Para obter mais informações sobre as funções de membro MDX, consulte [Referência da Função MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md).  
  
## <a name="tuple-functions"></a>funções de tupla  
 A linguagem MDX fornece várias funções que retornam tuplas e que podem ser usadas em qualquer lugar onde uma tupla é aceitada. Por exemplo, a função [Item &#40;Tupla&#41; &#40;MDX&#41;](../../../mdx/item-tuple-mdx.md) pode ser usada para extrair a primeira tupla do conjunto, o que é muito útil quando você sabe que um conjunto é composto por uma única tupla e quer fornecer essa tupla a uma função que requer uma tupla.  
  
 O exemplo a seguir retorna a primeira tupla do conjunto de tuplas do eixo de coluna.  
  
```  
SELECT {  
   ([Measures].[Reseller Sales Amount]  
      ,[Date].[Calendar Year].[CY 2003]  
   )  
, ([Measures].[Reseller Sales Amount]  
      ,[Date].[Calendar Year].[CY 2004]  
   )  
}.Item(0)  
ON COLUMNS   
FROM [Adventure Works]  
```  
  
 Para obter mais informações sobre as funções de tupla, consulte [Referência da Função MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md).  
  
## <a name="set-functions"></a>Funções do conjunto  
 A linguagem MDX fornece várias funções que retornam conjuntos. Digitar explicitamente tuplas e colocá-las entre chaves não é a única maneira de recuperar um conjunto. Para obter mais informações sobre a função de membros para retornar um conjunto, consulte [Principais conceitos em MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md). Há várias funções de conjunto adicionais.  
  
 O operador dois pontos permite o uso da ordem natural dos membros para criar um conjunto. Por exemplo, o conjunto mostrado no exemplo a seguir contém tuplas do primeiro ao quarto trimestre do ano calendário 2002.  
  
```  
SELECT   
   {[Calendar Quarter].[Q1 CY 2002]:[Calendar Quarter].[Q4 CY 2002]}   
ON 0  
FROM [Adventure Works]  
```  
  
 Se você não usar o operador dois pontos para criar o conjunto, pode criar o mesmo conjunto de membros especificando as tuplas do exemplo a seguir.  
  
```  
SELECT {  
   [Calendar Quarter].[Q1 CY 2002],   
   [Calendar Quarter].[Q2 CY 2002],   
   [Calendar Quarter].[Q3 CY 2002],   
   [Calendar Quarter].[Q4 CY 2002]  
   } ON 0  
FROM [Adventure Works]  
  
```  
  
 O operador dois pontos é uma função inclusiva. Os membros em ambos os lados do operador dois pontos são incluídos no conjunto resultante.  
  
 Para obter mais informações sobre as funções de conjunto, consulte [Referência da Função MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md).  
  
## <a name="array-functions"></a>Funções de matriz  
 Uma função de matriz age em um conjunto e retorna uma matriz. Para obter mais informações sobre as funções de matriz, consulte [Referência da Função MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md).  
  
## <a name="hierarchy-functions"></a>Funções de hierarquia  
 Uma função de hierarquia retorna uma hierarquia ao agir em um membro, um nível, uma hierarquia ou uma cadeia de caracteres. Para obter mais informações sobre as funções de hierarquia, consulte [Referência da Função MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md).  
  
## <a name="level-functions"></a>Funções de nível  
 Uma função nivelada retorna um nível ao agir em um membro, um nível ou uma cadeia de caracteres. Para obter mais informações sobre as funções de nível, consulte [Referência da Função MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md).  
  
## <a name="logical-functions"></a>Funções lógicas  
 Uma função lógica age em uma expressão MDX para retornar informações sobre tuplas, membros ou conjuntos da expressão. Por exemplo, a função [IsEmpty &#40;MDX&#41;](../../../mdx/isempty-mdx.md) avalia se uma expressão retornou um valor de célula vazio. Para obter mais informações sobre as funções lógicas, consulte [Referência de Função MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md).  
  
## <a name="numeric-functions"></a>Funções numéricas  
 Uma função numérica age em uma expressão MDX para retornar um valor escalar. Por exemplo, a função [Agregado &#40;MDX&#41;](../../../mdx/aggregate-mdx.md) retorna um valor escalar calculado agregando medidas sobre as tuplas de um conjunto especificado. Para obter mais informações sobre as funções numéricas, consulte [Referência de Função MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md).  
  
## <a name="string-functions"></a>Funções de cadeia de caracteres  
 A função de cadeia de caracteres age em uma expressão MDX para retornar uma cadeia de caracteres. Por exemplo, a função [UniqueName &#40;MDX&#41;](../../../mdx/uniquename-mdx.md) retorna um valor de cadeia de caracteres que contém o nome exclusivo de uma dimensão, uma hierarquia, um nível ou um membro. Para obter mais informações sobre as funções de cadeia de caracteres, consulte [Referência de Função MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md).  
  
## <a name="see-also"></a>Consulte também  
 [Principais conceitos em MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [Conceitos básicos de consulta MDX &#40; Analysis Services &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)   
 [Referência de função MDX &#40; MDX &#41;](../../../mdx/mdx-function-reference-mdx.md)  
  
  
