---
title: Esse (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: THIS
dev_langs: kbMDX
helpviewer_keywords: This function [MDX]
ms.assetid: 87acddee-ae54-49ee-8923-1b760606e8b7
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: cb9d77b3264b64af132a05fc73d82543060c9f19
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="this-mdx"></a>This (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o subcubo atual a ser usado com atribuições no script de cálculo de linguagem MDX.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
This   
```  
  
## <a name="remarks"></a>Comentários  
 O **isso** função pode ser usada no lugar de qualquer expressão de subcubo para fornecer o subcubo atual dentro do escopo atual do script de cálculo MDX. O **isso** função deve ser usada no lado esquerdo de uma atribuição.  
  
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
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [Cálculos](../analysis-services/multidimensional-models-olap-logical-cube-objects/calculations.md)  
  
  
