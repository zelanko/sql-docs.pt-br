---
title: Usando expressões escalares | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- scalar expressions
- expressions [MDX], scalar
ms.assetid: 4678b675-8fbd-4e5b-a519-d4cd1bb8c46a
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: a358a4a71b49cf36ba5537883a26abb80641f30f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="using-scalar-expressions"></a>Usando expressões escalares
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Na linguagem MDX, uma expressão escalar é um elemento da sintaxe MDX que, quando avaliado, retorna um único valor dentro do contexto de avaliação.  
  
 As expressões escalares incluem expressões de cadeia de caracteres, numéricas e de data em MDX.  
  
 As expressões escalares normalmente são usadas em definições de membro calculado, pois os membros calculados devem retornar um valor escalar. A consulta a seguir mostra exemplos de membros calculados na dimensão Medidas que usam tipos diferentes de expressão escalar:  
  
 `WITH`  
  
 `MEMBER MEASURES.NumericValue AS 10`  
  
 `MEMBER MEASURES.NumericExpression AS 10 + 10`  
  
 `MEMBER MEASURES.NumericExpressionBasedOnMeasure AS [Measures].[Internet Sales Amount] + 10`  
  
 `MEMBER MEASURES.StringValue AS "10"`  
  
 `MEMBER MEASURES.ConcatenatedString AS "10" + "10"`  
  
 `MEMBER MEASURES.StringFunction AS MEASURES.CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.TodaysDate AS NOW()`  
  
 `SELECT`  
  
 `{MEASURES.NumericValue,MEASURES.NumericExpression,MEASURES.NumericExpressionBasedOnMeasure,`  
  
 `MEASURES.StringValue, MEASURES.ConcatenatedString, MEASURES.StringFunction, MEASURES.TodaysDate}`  
  
 `ON COLUMNS`  
  
 `FROM [Adventure Works]`  
  
 O único tipo de dados que uma medida, um membro calculado ou outro elemento pode retornar é o tipo OLE VARIANT. Desse modo, às vezes pode ser necessário converter um valor de medida em um tipo específico para receber o comportamento esperado. A consulta a seguir mostra um exemplo disto:  
  
```  
WITH  
//Two calculated measures that return strings  
MEMBER MEASURES.NumericString1 AS "10"  
MEMBER MEASURES.NumericString2 AS "10"  
//In this case, the + operator acts to concatenate the strings  
MEMBER MEASURES.Concatenation AS MEASURES.NumericString1 + MEASURES.NumericString2  
//Casting one value to an integer with the CINT function causes the second measure  
//to be treated as an integer too, so that the + operator now acts to add the values  
MEMBER MEASURES.Addition AS CINT(MEASURES.NumericString1) + MEASURES.NumericString2  
SELECT  
{MEASURES.NumericString1,MEASURES.NumericString2,MEASURES.Concatenation,MEASURES.Addition }  
ON COLUMNS  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Expressões &#40;MDX&#41;](../mdx/expressions-mdx.md)  
  
  
