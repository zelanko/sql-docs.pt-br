---
title: '&gt;(Maior que) (MDX) | Microsoft Docs'
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: '>'
dev_langs: kbMDX
helpviewer_keywords:
- greater than operator (>)
- '> (greater than operator)'
ms.assetid: 36ba6462-5517-43be-8e7d-a38b7343c5d3
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: e99f087dd1aebb8235b317e10dc9368dbe17d561
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="gt-greater-than-mdx"></a>&gt;(Maior que) (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Realiza uma operação de comparação que determina se o valor de uma expressão MDX (Multidimensional Expressions) é maior do que o valor de outra expressão MDX.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
MDX_Expression > MDX_Expression  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *MDX_Expression*  
 Uma expressão MDX válida.  
  
## <a name="return-value"></a>Valor de retorno  
 Um valor booliano baseado nas seguintes condições:  
  
-   **True** se ambos os parâmetros forem não nulos e o primeiro parâmetro tiver um valor maior que o valor do segundo parâmetro.  
  
-   **False** se ambos os parâmetros forem não nulos e o primeiro parâmetro tiver um valor que seja igual ou inferior ao valor do segundo parâmetro.  
  
-   nulo se um ou os dois parâmetros forem avaliados como um valor nulo.  
  
## <a name="examples"></a>Exemplos  
 A consulta de exemplo a seguir demonstra o uso desse operador.  
  
```  
-- This query returns the gross profit margin (GPM)  
-- for Australia where the GPM is more than 50%.  
With Member [Measures].[HighGPM] as  
  IIF(  
      [Measures].[Gross Profit Margin] > .5,  
      [Measures].[Gross Profit Margin],  
      null)  
SELECT   
NON EMPTY [Sales Territory].[Sales Territory Country].[Australia] ON 0,  
    NON EMPTY [Product].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[HighGPM])  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de operador MDX &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
