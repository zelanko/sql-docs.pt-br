---
title: (Divide) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ba8cdf3a403d5673dc3114e88251f9b47f1f6e09
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63248192"
---
# <a name="divide---mdx-operator-reference"></a>Dividir - referência de operador MDX


  Realiza uma operação aritmética que divide um número por outro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Dividend / Divisor  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Dividend*  
 Uma linguagem MDX válida que retorna um valor numérico.  
  
 *Divisor*  
 Uma expressão MDX válida que retorna um valor numérico.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor com o tipo de dados do parâmetro com prioridade maior.  
  
## <a name="remarks"></a>Comentários  
 O valor real retornado pelo **/ (divisão)** operador representa o quociente da primeira expressão dividido pela segunda expressão.  
  
 As duas expressões devem ser do mesmo tipo de dados ou uma expressão deve poder ser convertida implicitamente no tipo de dados da outra expressão. Se *Divisor* é avaliada como um valor nulo, o operador gerará um erro. Se os dois *Divisor* e *dividendo* avaliar como um valor nulo, o operador retornará um valor nulo.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir demonstra o uso desse operador.  
  
```  
-- This query returns the freight cost per user,  
-- for products, averaged by month.   
With Member [Measures].[Freight Per Customer] as  
    [Measures].[Internet Freight Cost]  
    /   
    [Measures].[Customer Count]  
  
SELECT   
    [Ship Date].[Calendar].[Calendar Year] Members ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Freight Per Customer])  
```  
  
 Dividir um valor diferente de zero ou não nulo por zero ou nulo retornará o valor infinito, que é exibido nos resultados de consulta como o valor “1.#INF”. Na maioria dos casos, verifique se há divisão por zero para evitar esta situação. O exemplo a seguir mostra como:  
  
 `//Returns 1.#INF when Internet Sales Amount is zero or null`  
  
 `Member [Measures].[Reseller to Internet Ratio] AS`  
  
 `[Measures].[Reseller Sales Amount]`  
  
 `/`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `//Traps the division by zero scenario and returns null instead of 1.#INF`  
  
 `Member [Measures].[Reseller to Internet Ratio With Error Handling] AS`  
  
 `IIF([Measures].[Internet Sales Amount]=0, NULL,`  
  
 `[Measures].[Reseller Sales Amount]`  
  
 `/`  
  
 `[Measures].[Internet Sales Amount])`  
  
 `SELECT`  
  
 `{[Measures].[Reseller to Internet Ratio],[Measures].[Reseller to Internet Ratio With Error Handling]} ON 0,`  
  
 `[Product].[Category].[Category].Members ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 `WHERE([Date].[Calendar].[Calendar Year].&[2001])`  
  
## <a name="see-also"></a>Consulte também  
 [IIf &#40;MDX&#41;](../mdx/iif-mdx.md)   
 [Referência de operador MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
