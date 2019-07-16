---
title: Exceto (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d53a88ce78eb5a1b106cefb0832ca1023f67c000
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077256"
---
# <a name="except-mdx-function"></a>Exceto a função (MDX)


  Avalia dois conjuntos e remove as tuplas do primeiro conjunto e também existem no segundo, mantendo as duplicações (opcional).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Except(Set_Expression1, Set_Expression2 [, ALL ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression1*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Set_Expression2*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
## <a name="remarks"></a>Comentários  
 Se **todos os** é especificado, a função preservará as duplicações encontradas no primeiro conjunto; as duplicações encontradas no segundo conjunto ainda serão removidas. Os membros são retornados na ordem em que aparecem no primeiro conjunto.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir demonstra o uso dessa função.  
  
```  
   //This query shows the quantity of orders for all products,  
   //with the exception of Components, which are not  
   //sold.  
SELECT   
   [Date].[Month of Year].Children  ON COLUMNS,  
   Except  
      ([Product].[Product Categories].[All].Children ,  
         {[Product].[Product Categories].[Components]}  
      ) ON ROWS  
FROM  
   [Adventure Works]  
WHERE  
   ([Measures].[Order Quantity])  
```  
  
## <a name="see-also"></a>Consulte também  
 [- &#40;Exceto&#41; &#40;MDX&#41;](../mdx/except-mdx-operator.md)   
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
