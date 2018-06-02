---
title: Usando expressões de dimensão | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f680c5478eb1ee03fd69506d669fbc49c91c0241
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34582488"
---
# <a name="using-dimension-expressions"></a>Usando expressões de dimensão
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Normalmente, expressões de dimensão e hierarquia são usadas ao passar parâmetros para funções em linguagem MDX para retornar membros, conjuntos ou tuplas a partir de uma hierarquia.  
  
 Expressões de dimensão só podem ser expressões simples porque elas são identificadores de objetos. Consulte [expressões &#40;MDX&#41; ](../mdx/expressions-mdx.md) para obter uma explicação de expressões simples e complexas.  
  
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
  
 Um identificador de hierarquia aparece como *Dimension_Name **.** Hierarchy_Name* na notação BNF usada para descrever instruções MDX.  
  
## <a name="see-also"></a>Consulte também  
 [Expressões &#40;MDX&#41;](../mdx/expressions-mdx.md)  
  
  
