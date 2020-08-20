---
description: Instrução CASE (MDX)
title: Instrução CASE (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7a5907eb58fa102c46fa22af97116c4fad0f217a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466498"
---
# <a name="case-statement-mdx"></a>Instrução CASE (MDX)


  Permite retornar de modo condicional valores específicos de várias comparações. Há dois tipos de instruções CASE:  
  
-   Uma instrução CASE simples que compara uma expressão com um conjunto de expressões simples para retornar valores específicos.  
  
-   Uma instrução CASE pesquisada que avalia um conjunto de expressões boolianas para retornar valores específicos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Simple Case Statement  
CASE [input_expression]  
WHEN when_expression THEN when_true_result_expression  
[...n]  
[ELSE else_result_expression]  
END  
  
Search Case Statement  
CASE   
WHEN Boolean_expression THEN when_true_result_expression  
[...n]  
[ELSE else_result_expression]  
END  
```  
  
## <a name="arguments"></a>Argumentos  
 *input_expression*  
 Uma expressão MDX (Multidimensional Expressions) resolvida em um valor escalar.  
  
 *when_expression*  
 Um valor escalar especificado em relação ao qual o *input_expression* é avaliado, que, quando avaliado como true, retorna o valor escalar da *else_result_expression*.  
  
 *when_true_result_expression*  
 O valor escalar retornado quando a cláusula WHEN é avaliada como true.  
  
 *else_result_expression*  
 O valor escalar retornado quando nenhuma cláusula WHEN é avaliada como true.  
  
 *Boolean_expression*  
 Uma expressão MDX avaliada como um valor escalar.  
  
## <a name="remarks"></a>Comentários  
 Se não houver nenhuma cláusula ELSE e todas as cláusulas WHEN forem avaliadas como false, o resultado será uma célula vazia.  
  
## <a name="simple-case-expression"></a>Expressão CASE simples  
 A linguagem MDX avalia uma expressão CASE simples resolvendo o *input_expression* para um valor escalar. Esse valor escalar é comparado com o valor escalar do *when_expression*. Se os dois valores escalares corresponderem, a instrução CASE retornará o valor da *when_true_expression*. Se os dois valores escalares não coincidirem, a próxima cláusula WHEN será avaliada. Se todas as cláusulas WHEN forem avaliadas como false, o valor de *else_result_expression* da cláusula else, se houver, será retornado.  
  
 No exemplo a seguir, a medida Contagem dos Pedidos do Revendedor é avaliada em várias cláusulas WHEN e retorna um resultado com base no valor da medida Contagem dos Pedidos do Revendedor de cada ano. Para valores de contagem de pedidos de revendedor que não correspondem a um valor escalar especificado em uma *when_expression* em uma cláusula WHEN, o valor escalar da *else_result_expression* é retornado.  
  
```  
WITH MEMBER [Measures].x AS   
CASE [Measures].[Reseller Order Count]  
   WHEN 0 THEN 'NONE'  
   WHEN 1 THEN 'SMALL'  
   WHEN 2 THEN 'SMALL'  
   WHEN 3 THEN 'MEDIUM'  
   WHEN 4 THEN 'MEDIUM'  
   WHEN 5 THEN 'LARGE'  
   WHEN 6 THEN 'LARGE'  
      ELSE 'VERY LARGE'  
END  
SELECT Calendar.[Calendar Year] on 0  
, NON EMPTY [Geography].[Postal Code].Members ON 1  
FROM [Adventure Works]  
WHERE [Measures].x  
```  
  
## <a name="searched-case-expression"></a>Expressão CASE pesquisada  
 Para usar a expressão CASE para executar avaliações mais complexas, use a expressão CASE pesquisada. Essa variação da expressão de pesquisa permite que você avalie se uma expressão de entrada está dentro de um intervalo de valores. O MDX avalia as cláusulas WHEN para que essas cláusulas apareçam na instrução CASE.  
  
 No exemplo a seguir, a medida contagem de pedidos do revendedor é avaliada em relação ao *Boolean_expression* especificado para cada uma das várias cláusulas WHEN. O resultado é retornado com base no valor da medida Contagem dos Pedidos do Revendedor de cada ano. Como as cláusulas WHEN são avaliadas na ordem em que aparecem, todos os valores superiores a 6 podem receber facilmente o valor “VERY LARGE”, sem ser necessário especificar cada valor explicitamente. Para os valores de contagem de pedidos do revendedor que não são especificados em uma cláusula WHEN, o valor escalar da *else_result_expression* é retornado.  
  
```  
WITH MEMBER [Measures].x AS   
CASE   
   WHEN [Measures].[Reseller Order Count] > 6 THEN 'VERY LARGE'  
   WHEN [Measures].[Reseller Order Count] > 4 THEN 'LARGE'  
   WHEN [Measures].[Reseller Order Count] > 2 THEN 'MEDIUM'  
   WHEN [Measures].[Reseller Order Count] > 0 THEN 'SMALL'  
   ELSE "NONE"  
END  
SELECT Calendar.[Calendar Year] on 0,  
NON EMPTY [Geography].[Postal Code].Members on 1  
FROM [Adventure Works]  
WHERE [Measures].x  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções de script MDX &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
