---
title: Acumulado no ano (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- YTD
dev_langs:
- kbMDX
helpviewer_keywords:
- Ytd function
ms.assetid: b77fdba2-d4a9-4271-8c21-c1f12eba526d
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: b647c31febd5ef06b8cb2e6f808e296518f98af6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
 [Referência de função MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
