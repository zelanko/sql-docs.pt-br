---
title: '&gt;= (Maior ou igual a) (MDX) | Microsoft Docs'
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: '>='
dev_langs: kbMDX
helpviewer_keywords:
- '>= (greater than or equal to operator)'
- greater than or equal to (>=)
ms.assetid: 272f4614-9ba3-46bd-8306-181c26e798f1
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 5f35e30a0ffe87e30641f8382728eb2401ac478c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="gt-greater-than-or-equal-to-mdx"></a>&gt;= (Maior ou igual a) (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Realiza uma operação de comparação que determina se o valor de uma expressão MDX (Multidimensional Expressions) fé maior ou igual ao valor de outra expressão MDX.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
MDX_Expression >= MDX_Expression  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *MDX_Expression*  
 Uma expressão MDX válida.  
  
## <a name="return-value"></a>Valor de retorno  
 Um valor booliano baseado nas seguintes condições:  
  
-   **True** se o primeiro parâmetro tiver um valor que é maior que ou igual ao valor do segundo parâmetro.  
  
-   **False** se o primeiro parâmetro tiver um valor menor que o valor do segundo parâmetro.  
  
-   **True** se ambos os parâmetros forem nulos ou se um parâmetro for nulo e o outro parâmetro é 0.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir demonstra o uso desse operador.  
  
```  
-- This query returns the gross profit margin (GPM)  
-- for Australia where the GPM is greater than or equal to 50%.  
With Member [Measures].[HighGPM] as  
  IIF(  
      [Measures].[Gross Profit Margin] >= .5,  
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
  
  
