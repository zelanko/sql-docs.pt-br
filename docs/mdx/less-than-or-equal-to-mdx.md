---
title: '&lt;= (Menor ou igual a) (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 02f6990698603efdf813e244d11e57c3bd6bb7eb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63311895"
---
# <a name="lt-less-than-or-equal-to-mdx"></a>&lt;= (Menor ou igual a) (MDX)


  Realiza uma operação de comparação que determina se o valor de uma expressão MDX (Multidimensional Expressions) é menor ou igual ao valor de outra expressão MDX.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
MDX_Expression <= MDX_Expression  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *MDX_Expression*  
 Uma expressão MDX válida.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor booliano baseado nas seguintes condições:  
  
-   t**rue** se ambos os parâmetros forem não nulos e o primeiro parâmetro tiver um valor que seja menor ou igual ao valor do segundo parâmetro.  
  
-   f**alse** se ambos os parâmetros forem não nulos e o primeiro parâmetro tiver um valor que maior que o valor do segundo parâmetro.  
  
-   nulo se um ou os dois parâmetros forem avaliados como um valor nulo.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir demonstra o uso desse operador.  
  
```  
-- This query returns the gross profit margin (GPM)  
-- for Australia where the GPM is less than or equal to 30%.  
With Member [Measures].[LowGPM] as  
  IIF(  
      [Measures].[Gross Profit Margin] <= .5,  
      [Measures].[Gross Profit Margin],  
      null)  
SELECT   
NON EMPTY [Sales Territory].[Sales Territory Country].[Australia] ON 0,  
    NON EMPTY [Product].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[LowGPM])  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de operador MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
