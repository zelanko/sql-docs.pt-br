---
title: Esse (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 77db403ee016283a565a6bc86d2f6857de0eff45
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63259025"
---
# <a name="this-mdx"></a>This (MDX)


  Retorna o subcubo atual a ser usado com atribuições no script de cálculo de linguagem MDX.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
This   
```  
  
## <a name="remarks"></a>Comentários  
 O **isso** função pode ser usada no lugar de qualquer expressão de subcubo para fornecer o subcubo atual dentro do escopo atual dentro do script de cálculo MDX. O **isso** função deve ser usada no lado esquerdo de uma atribuição.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Cálculos](../analysis-services/multidimensional-models-olap-logical-cube-objects/calculations.md)  
  
  
