---
title: '- (Exceto) (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cf0121d1be3cd2943a801f3c72ca4952b70ec681
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139078"
---
# <a name="except-mdx-operator"></a>Exceto o operador (MDX)


  Executa uma operação definida que retorna a diferença entre dois conjuntos, removendo membros duplicados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set_Expression - Set_Expression  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
## <a name="return-value"></a>Valor retornado  
 Um conjunto que contém membros que não são compartilhados pelos parâmetros especificados.  
  
## <a name="remarks"></a>Comentários  
 O **- (exceto)** operador é funcionalmente equivalente de [exceto](../mdx/except-mdx-function.md) função.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência de operador MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
