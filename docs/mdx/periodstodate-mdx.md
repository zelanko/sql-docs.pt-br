---
title: PeriodsToDate (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 812cd16a7d6b7a17d4f2f12098f22e32cf0d3363
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68055633"
---
# <a name="periodstodate-mdx"></a>PeriodsToDate (MDX)


  Retorna um conjunto de membros irmão do mesmo nível como um determinado membro, começando com o primeiro irmão e terminando com um determinado membro, restringido por um nível especificado na dimensão Tempo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
PeriodsToDate( [ Level_Expression [ ,Member_Expression ] ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Level_Expression*  
 Uma linguagem MDX válida que retorna um nível.  
  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Comentários  
 Dentro do escopo do nível especificado, a função **PeriodsToDate** retorna o conjunto de períodos no mesmo nível do membro especificado, começando com o primeiro período e terminando com o membro especificado.  
  
-   Se um nível for especificado, o membro atual da hierarquia será a *hierarquia*deduzida. **CurrentMember**, em que *hierarquia*é a hierarquia do nível especificado.  
  
-   Se nem o nível nem o membro for especificado, o nível será o nível pai do membro atual da primeira hierarquia na primeira dimensão do tipo Tempo no grupo de medidas.  
  
 
  `PeriodsToDate( Level_Expression, Member_Expression )` é funcionalmente equivalente à seguinte linguagem MDX:  
  
 `TopCount(Descendants(Ancestor(Member_Expression, Level_Expression), Member_Expression.Level), 1):Member_Expression`  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a soma do `Measures.[Order Quantity]` membro, agregados nos primeiros oito meses do ano civil 2003 que estão contidos na `Date` dimensão, do cubo **Adventure Works** .  
  
```  
WITH MEMBER [Date].[Calendar].[First8Months2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Year],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First8Months2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 O exemplo a seguir mostra a agregação durante os primeiros dois meses do segundo semestre do ano calendário 2003.  
  
```  
WITH MEMBER [Date].[Calendar].[First2MonthsSecondSemester2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Semester],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First2MonthsSecondSemester2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [TopCount&#41;MDX &#40;](../mdx/topcount-mdx.md)   
 [Referência de função MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
