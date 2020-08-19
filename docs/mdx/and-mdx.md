---
description: AND (MDX)
title: E (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: baff2f517f5fdd6dfbb23eb24ad51ed12589df52
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429968"
---
# <a name="and-mdx"></a>AND (MDX)


  Realiza uma conjunção lógica em duas expressões numéricas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Expression1 AND Expression2  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Expression1*  
 Uma linguagem MDX válida que retorna um valor numérico.  
  
 *Expression2*  
 Uma expressão MDX válida que retorna um valor numérico.  
  
## <a name="return-value"></a>Valor de retorno  
 Um valor booliano que retornará true se ambos os parâmetros forem avaliados como **true**; caso contrário, **false**.  
  
## <a name="remarks"></a>Comentários  
 O operador **and** trata as expressões como valores Boolianos (zero, 0, como **false**; caso contrário, **true**) antes que o operador execute a conjunção lógica. A tabela a seguir ilustra como o operador **and** executa a conjunção lógica.  
  
|*Expression1*|*Expression2*|Valor de retorno|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**true**|  
|**true**|**false**|**false**|  
|**false**|**true**|**false**|  
|**false**|**false**|**false**|  
  
## <a name="example"></a>Exemplo  
  
```  
-- This query returns the gross profit margin (GPM)  
-- for clothing sales where the GPM is between 20% and 30%.  
With Member [Measures].[LowGPM] as  
  IIF(  
      [Measures].[Gross Profit Margin] <= .3 AND   
      [Measures].[Gross Profit Margin] >= .2,  
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
 [Referência de operador MDX &#40;&#41;MDX ](../mdx/mdx-operator-reference-mdx.md)  
  
  
