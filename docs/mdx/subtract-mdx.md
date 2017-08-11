---
title: "- (Subtração) (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '-'
dev_langs:
- kbMDX
helpviewer_keywords:
- '- (subtract)'
- subtract operator (-)
ms.assetid: 56e610a1-efbd-4c11-bd7c-bf20a6553e57
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e227e969b36d4ac41d54c2cfd291364bb22650fb
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="--subtract-mdx"></a>- (Subtração) (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Realiza uma operação aritmética que subtrai um número do outro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Numeric_Expression - Numeric_Expression  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Numeric_Expression*  
 Uma linguagem MDX válida que retorna um valor numérico.  
  
## <a name="return-value"></a>Valor de retorno  
 Um valor com o tipo de dados do parâmetro com prioridade maior.  
  
## <a name="remarks"></a>Comentários  
 As duas expressões devem ser do mesmo tipo de dados ou uma expressão deve poder ser convertida implicitamente no tipo de dados da outra expressão. Se uma expressão for avaliada como um valor nulo, o operador retornará o resultado da expressão não nula.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir demonstra o uso desse operador.  
  
```  
-- This member returns the increase or decrease  
-- in gross profit margin over a month.  
WITH MEMBER [Measures].[GPM Delta] AS  
 (  
(Measures.[Gross Profit Margin]) -   
([Date].[Calendar].CurrentMember.PrevMember,   
Measures.[Gross Profit Margin])  
  ), FORMAT_STRING = 'Percent'  
  
SELECT   
DESCENDANTS(  
[Date].[Calendar].[Calendar Year].&[2002],   
[Date].[Calendar].[Month]) ON 0,  
[Product].[Category].[Category].Members ON 1  
FROM  
[Adventure Works]  
WHERE  
([Measures].[GPM Delta])  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de operador MDX &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  

