---
title: Ytd (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 67df625611f2451c3442d5d59b56c76dfc14a74a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63295156"
---
# <a name="ytd-mdx"></a>Ytd (MDX)


  Retorna os membros de um conjunto de irmãos do mesmo nível de um determinado membro, começando com o primeiro irmão e terminando com um determinado membro, restringido pelo *ano* nível na dimensão de tempo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Ytd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Comentários  
 Se uma expressão de membro não for especificada, o padrão é o membro atual da primeira hierarquia com um nível de tipo *anos* na primeira dimensão do tipo *tempo* no grupo de medidas.  
  
 O **Ytd** é uma função de atalho para o [PeriodsToDate](../mdx/periodstodate-mdx.md) função em que a propriedade de tipo da hierarquia de atributo no qual o nível é baseado é definida como *anos*. Ou seja, `Ytd(Member_Expression)` é equivalente a `PeriodsToDate(Year_Level_Expression,Member_Expression)`. Observe que essa função não funcionará quando a propriedade Type é definida como *FiscalYears*.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna a soma do `Measures.[Order Quantity]` membro, agregado durante os primeiros oito meses do ano calendário 2003 contidos na `Date` dimensão, da **Adventure Works** cubo.  
  
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
  
 **Acumulado no ano** é usado frequentemente em combinação com nenhum parâmetro especificado, o que significa que o [CurrentMember &#40;MDX&#41; ](../mdx/currentmember-mdx.md) função exibirá um total acumulado de year-to-date em um relatório, conforme mostrado no consulta a seguir:  
  
 `WITH MEMBER MEASURES.YTDDEMO AS`  
  
 `AGGREGATE(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDDEMO} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
