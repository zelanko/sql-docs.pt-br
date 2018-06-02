---
title: Acumulado no ano (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 33deba1261ad6c2afcf44854b0590c978683f08b
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581880"
---
# <a name="ytd-mdx"></a>Ytd (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna um conjunto de irmãos membros do mesmo nível de um determinado membro, começando com o primeiro irmão e terminando com um determinado membro, restringido pelo *ano* nível na dimensão de tempo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Ytd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Remarks  
 Se uma expressão de membro não for especificada, o padrão será o membro atual da primeira hierarquia com um nível de tipo *anos* na primeira dimensão do tipo *tempo* no grupo de medidas.  
  
 O **Ytd** é uma função de atalho para o [PeriodsToDate](../mdx/periodstodate-mdx.md) função onde a propriedade de tipo da hierarquia de atributo no qual o nível é baseado é definida como *anos*. Ou seja, `Ytd(Member_Expression)` é equivalente a `PeriodsToDate(Year_Level_Expression,Member_Expression)`. Observe que essa função não funcionará quando a propriedade de tipo é definida como *FiscalYears*.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna a soma da `Measures.[Order Quantity]` membro, agregado sobre os primeiros oito meses do ano calendário 2003 contidos no `Date` dimensão, do **Adventure Works** cubo.  
  
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
  
 **Acumulado no ano** é frequentemente usado em combinação com parâmetros especificados, o que significa que o [CurrentMember &#40;MDX&#41; ](../mdx/currentmember-mdx.md) função exibirá um total acumulado do ano até a data em um relatório, conforme mostrado do consulta a seguir:  
  
 `WITH MEMBER MEASURES.YTDDEMO AS`  
  
 `AGGREGATE(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDDEMO} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
