---
title: "Usando expressões de dimensão | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords:
- expressions [MDX], dimensions
- dimensions [Analysis Services], MDX
ms.assetid: 1d40cffb-e88f-4284-93cf-d62ab4f08395
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 1417fd747df92c84fe66e2c69996f57ab51875e1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="using-dimension-expressions"></a>Usando expressões de dimensão
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Normalmente, expressões de dimensão e hierarquia são usadas ao passar parâmetros para funções em linguagem MDX para retornar membros, conjuntos ou tuplas a partir de uma hierarquia.  
  
 Expressões de dimensão só podem ser expressões simples porque elas são identificadores de objetos. Consulte [expressões &#40; MDX &#41; ](../mdx/expressions-mdx.md) para obter uma explicação de expressões simples e complexas.  
  
## <a name="dimension-expressions"></a>Expressões de dimensão  
 Uma expressão de dimensão contém um identificador de dimensão ou uma função de dimensão.  
  
 As expressões de dimensão raramente são usadas automaticamente. Em vez disso, você normalmente especifica uma hierarquia em uma dimensão. A única exceção é quando você estar trabalhando com a dimensão Medidas, que não tem nenhuma hierarquia.  
  
 O exemplo a seguir mostra um membro calculado que usa a expressão [Measures] junto com as funções .Members e Count() para retornar o número de membros na dimensão Medidas:  
  
 `WITH MEMBER [Measures].[MeasureCount] AS`  
  
 `COUNT([Measures].MEMBERS)`  
  
 `SELECT [Measures].[MeasureCount] ON 0`  
  
 `FROM [Adventure Works]`  
  
 Um identificador de dimensão aparece como *Dimension_Name* na notação BNF usada para descrever instruções MDX.  
  
## <a name="hierarchy-expressions"></a>Expressões de hierarquia  
 De modo similar, uma expressão de hierarquia contém um identificador de hierarquia ou uma função de hierarquia. O exemplo a seguir mostra o uso da expressão de hierarquia [Date].[Calendar], junto com as funções .Levels e .Count, para retornar o número de níveis na hierarquia Calendário da dimensão Data:  
  
 `WITH MEMBER [Measures].[CalendarLevelCount] AS`  
  
 `[Date].[Calendar].Levels.Count`  
  
 `SELECT [Measures].[CalendarLevelCount] ON 0`  
  
 `FROM [Adventure Works]`  
  
 O cenário mais comum onde são usadas expressões de hierarquia está relacionado à função .Members para retornar todos os membros em uma hierarquia. O exemplo a seguir retorna todos os membros de [Date].[Calendar] no eixo de linhas:  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 Um identificador de hierarquia aparece como *Dimension_Name**.* *Hierarchy_Name* na notação BNF usada para descrever instruções MDX.  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões &#40; MDX &#41;](../mdx/expressions-mdx.md)  
  
  
