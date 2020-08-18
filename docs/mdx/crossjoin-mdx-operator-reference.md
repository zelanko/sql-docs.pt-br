---
description: Referência de operador de interjunção-MDX
title: '* Junção (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c957b72736fa8038f01175e3c65898a85704a56b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88413142"
---
# <a name="crossjoin----mdx-operator-reference"></a>Referência de operador de interjunção-MDX


  Executa uma operação definida que retorna o produto cruzado de dois conjuntos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set_Expression * Set_Expression  
```  
  
## <a name="parameter"></a>Parâmetro  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
## <a name="return-value"></a>Valor de retorno  
 Um conjunto que contém o produto cruzado de ambos os parâmetros especificados.  
  
## <a name="remarks"></a>Comentários  
 O operador ** \* (interjunção)** é funcionalmente equivalente à função de [interjunção](../mdx/crossjoin-mdx.md) .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir demonstra o uso desse operador.  
  
```  
-- This query returns the gross profit margin for product types  
-- and reseller types crossjoined by year.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
    [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Gross Profit Margin])  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de operador MDX &#40;&#41;MDX ](../mdx/mdx-operator-reference-mdx.md)  
  
  
