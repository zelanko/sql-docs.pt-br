---
title: Operadores unários | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8d90a8380c29fd6d77126cd6ca8a0ec93634db39
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581398"
---
# <a name="unary-operators"></a>Operadores unários
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Na linguagem MDX, os operadores unários executam uma operação em um operando único, como retornar o valor negativo ou positivo de uma expressão numérica.  
  
 O MDX oferece suporte aos operadores unários listados na tabela a seguir.  
  
|Operador|Description|  
|--------------|-----------------|  
|[- (Negativo)](../mdx/negative-mdx.md)|Retorna o valor negativo de uma expressão numérica.|  
|[+ (Positivo)](../mdx/positive-mdx.md)|Retorna o valor positivo de uma expressão numérica.|  
  
 O exemplo a seguir demonstra o uso de um operador unário para retornar o valor negativo de uma medida:  
  
```  
WITH   
   MEMBER [Measures].[NegDiscountAmount] AS  
   -[Measures].[Discount Amount]  
SELECT   
   {[Measures].[Discount Amount],[Measures].[NegDiscountAmount]} on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
```  
  
 Além disso, o MDX usa operadores unários especiais para determinar a operação de agregação executada pelo [RollupChildren](../mdx/rollupchildren-mdx.md) função. Para obter mais informações sobre estes operadores unários especiais, consulte [adicionar uma agregação personalizada a uma dimensão](../analysis-services/multidimensional-models/bi-wizard-add-a-custom-aggregation-to-a-dimension.md).  
  
## <a name="see-also"></a>Consulte também  
 [Operadores &#40;sintaxe MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
  
