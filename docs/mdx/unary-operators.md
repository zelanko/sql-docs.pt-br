---
description: Operadores unários
title: Operadores unários | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 391b39dd92011ce43b146d740b232d0c4fca6669
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193476"
---
# <a name="unary-operators"></a>Operadores unários


  Na linguagem MDX, os operadores unários executam uma operação em um operando único, como retornar o valor negativo ou positivo de uma expressão numérica.  
  
 O MDX oferece suporte aos operadores unários listados na tabela a seguir.  
  
|Operador|Descrição|  
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
  
 Além disso, o MDX usa operadores unários especiais para determinar a operação de agregação executada pela função [RollupChildren](../mdx/rollupchildren-mdx.md) . Para obter mais informações sobre esses operadores unários especiais, consulte [Adicionar uma agregação personalizada a uma dimensão](/analysis-services/multidimensional-models/bi-wizard-add-a-custom-aggregation-to-a-dimension).  
  
## <a name="see-also"></a>Consulte Também  
 [Operadores &#40;sintaxe MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
