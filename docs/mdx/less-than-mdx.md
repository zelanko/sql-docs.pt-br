---
title: '&lt;(Menor que) (MDX) | Microsoft Docs'
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
- <
dev_langs:
- kbMDX
helpviewer_keywords:
- less than (<)
- < (less than operator)
ms.assetid: 53d86151-230b-4061-916f-ca8bb172d21e
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 99be3c9f3896f84dbee770859c14725f299b63ff
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="lt-less-than-mdx"></a>&lt;(Menor que) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Realiza uma operação de comparação que determina se o valor de uma expressão MDX (Multidimensional Expressions) é menor do que o valor de outra expressão MDX.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
MDX_Expression < MDX_Expression  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *MDX_Expression*  
 Uma expressão MDX válida.  
  
## <a name="return-value"></a>Valor de retorno  
 Um valor booliano baseado nas seguintes condições:  
  
-   **True** se ambos os parâmetros forem não nulos e o primeiro parâmetro tiver um valor menor que o valor do segundo parâmetro.  
  
-   **False** se ambos os parâmetros forem não nulos e o primeiro parâmetro tiver um valor que seja igual ou maior que o valor do segundo parâmetro.  
  
-   nulo se um ou os dois parâmetros forem avaliados como um valor nulo.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir demonstra o uso desse operador.  
  
```  
-- This query returns the gross profit margin (GPM)  
-- for clothing sales where the GPM is less than 30%.  
With Member [Measures].[LowGPM] as  
  IIF(  
      [Measures].[Gross Profit Margin] < .3,  
      [Measures].[Gross Profit Margin],  
      null)  
SELECT NON EMPTY  
    [Sales Territory].[Sales Territory Country].Members ON 0,  
    [Product].[Category].[Clothing] ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[LowGPM])  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de operador MDX &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
