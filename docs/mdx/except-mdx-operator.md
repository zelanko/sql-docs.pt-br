---
title: '- (Exceto) (MDX) | Microsoft Docs'
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- '-'
dev_langs:
- kbMDX
helpviewer_keywords:
- Except operator [MDX]
- '- (except operator)'
ms.assetid: 8971a09d-b254-4c4c-a099-103664783589
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 17fd5aa25df6119e7b848b2ad06d00d6daeb31af
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="except-mdx-operator"></a>Exceto operador (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Remarks  
 O **- (exceto)** operador é funcionalmente equivalente ao [exceto](../mdx/except-mdx-function.md) função.  
  
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
  
  
