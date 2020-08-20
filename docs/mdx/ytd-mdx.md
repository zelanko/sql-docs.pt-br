---
description: Ytd (MDX)
title: Acumulado no ano (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 14f286a304e03624a9ce20c1bd7b045dffc38688
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491364"
---
# <a name="ytd-mdx"></a>Ytd (MDX)


  Retorna um conjunto de membros irmãos do mesmo nível de um determinado membro, começando com o primeiro irmão e terminando com o membro determinado, como restrito pelo nível de *ano* na dimensão de tempo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Ytd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Comentários  
 Se uma expressão de membro não for especificada, o padrão será o membro atual da primeira hierarquia com um nível do tipo *Years* na primeira dimensão do tipo *time* no grupo de medidas.  
  
 A função timeyear é **uma função de** atalho para a função [PeriodsToDate](../mdx/periodstodate-mdx.md) em que a propriedade Type da hierarquia de atributo na qual o nível é baseado é definida como *Years*. Ou seja, `Ytd(Member_Expression)` é equivalente a `PeriodsToDate(Year_Level_Expression,Member_Expression)`. Observe que essa função não funcionará quando a propriedade Type for definida como *FiscalYears*.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna a soma do `Measures.[Order Quantity]` membro, agregados nos primeiros oito meses do ano civil 2003 que estão contidos na `Date` dimensão, do cubo **Adventure Works** .  
  
```  
WITH MEMBER [Date].[Calendar].[First8MonthsCY2003] AS  
    Aggregate(  
        YTD([Date].[Calendar].[Month].[August 2003])  
    )  
SELECT   
    [Date].[Calendar].[First8MonthsCY2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 O **ano** é frequentemente usado em combinação sem parâmetros especificados, o que significa que a função [CurrentMember &#40;MDX&#41;](../mdx/currentmember-mdx.md) exibirá um total acumulado no ano até a data em um relatório, conforme mostrado na seguinte consulta:  
  
 `WITH MEMBER MEASURES.YTDDEMO AS`  
  
 `AGGREGATE(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDDEMO} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
