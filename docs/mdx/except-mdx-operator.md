---
description: Operador Except (MDX)
title: '- Excepção (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f45c01cb4a2c3e4383790637b6603f789048078d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341492"
---
# <a name="except-mdx-operator"></a>Operador Except (MDX)


  Executa uma operação definida que retorna a diferença entre dois conjuntos, removendo membros duplicados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set_Expression - Set_Expression  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
## <a name="return-value"></a>Valor de retorno  
 Um conjunto que contém membros que não são compartilhados pelos parâmetros especificados.  
  
## <a name="remarks"></a>Comentários  
 O operador **-(except)** é funcionalmente equivalente à função [Except](../mdx/except-mdx-function.md) .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir demonstra o uso desse operador:  
  
```  
// This query shows the quantity of orders for all product categories  
// with the exception of Components.  
SELECT   
   [Measures].[Order Quantity] ON COLUMNS,  
   [Product].[Product Categories].[All].Children   
   - [Product].[Product Categories].[Components] ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de operador MDX &#40;&#41;MDX ](../mdx/mdx-operator-reference-mdx.md)  
  
  
