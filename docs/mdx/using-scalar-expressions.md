---
title: Usando expressões escalares | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b87fad1b9c568f4ebd5f65ef3705001b12d26693
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68038042"
---
# <a name="using-scalar-expressions"></a>Usando expressões escalares


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
  
## <a name="see-also"></a>Consulte Também  
 [Expressões &#40;MDX&#41;](../mdx/expressions-mdx.md)  
  
  
