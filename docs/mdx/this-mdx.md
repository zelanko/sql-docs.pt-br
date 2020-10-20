---
description: This (MDX)
title: Este (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b55a416a14d0b837d134e7f9d8520d77cc13e375
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192326"
---
# <a name="this-mdx"></a>This (MDX)


  Retorna o subcubo atual a ser usado com atribuições no script de cálculo de linguagem MDX.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
This   
```  
  
## <a name="remarks"></a>Comentários  
 A função **this** pode ser usada no lugar de qualquer expressão de subcubo para fornecer o subcubo atual dentro do escopo atual dentro do script de cálculo MDX. A função **this** deve ser usada no lado esquerdo de uma atribuição.  
  
## <a name="examples"></a>Exemplos  
 O fragmento de script MDX a seguir mostra como a palavra-chave This pode ser usada com instruções SCOPE para fazer atribuições a subcubos:  
  
 `Scope`  
  
 `(`  
  
 `[Date].[Fiscal Year].&[2005],`  
  
 `[Date].[Fiscal].[Fiscal Quarter].Members,`  
  
 `[Measures].[Sales Amount Quota]`  
  
 `) ;`  
  
 `This = ParallelPeriod`  
  
 `(`  
  
 `[Date].[Fiscal].[Fiscal Year], 1,`  
  
 `[Date].[Fiscal].CurrentMember`  
  
 `) * 1.35 ;`  
  
 `/*-- Allocate equally to months in FY 2002 -----------------------------*/`  
  
 `Scope`  
  
 `(`  
  
 `[Date].[Fiscal Year].&[2002],`  
  
 `[Date].[Fiscal].[Month].Members`  
  
 `) ;`  
  
 `This = [Date].[Fiscal].CurrentMember.Parent / 3 ;`  
  
 `End Scope ;`  
  
 `End Scope;`  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40;&#41;MDX ](../mdx/mdx-function-reference-mdx.md)   
 [Cálculos](/analysis-services/multidimensional-models-olap-logical-cube-objects/calculations)  
  
