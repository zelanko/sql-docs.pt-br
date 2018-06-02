---
title: Qtd (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 218e90b5e43a1603978ba912fccb85ae16b34072
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580918"
---
# <a name="qtd-mdx"></a>Qtd (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna um conjunto de irmãos membros do mesmo nível de um determinado membro, começando com o primeiro irmão e terminando com um determinado membro, restringido pelo *trimestre* nível na dimensão de tempo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Qtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Remarks  
 Se um expressionis de membro não especificado, o padrão será o membro atual da primeira hierarquia com um nível de tipo *trimestres* na primeira dimensão do tipo *tempo* no grupo de medidas.  
  
 O **Qtd** é uma função de atalho para o [PeriodsToDate &#40;MDX&#41; ](../mdx/periodstodate-mdx.md) função cujo argumento de expressão de nível é definido como *trimestre*. Ou seja, `Qtd(Member_Expression)` é funcionalmente equivalente a `PeriodsToDate(Quarter_Level_Expression, Member_Expression)`.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna a soma da `Measures.[Order Quantity]` membro, agregado sobre os primeiros dois meses do terceiro trimestre do ano calendário 2003 contidos no `Date` dimensão, do **Adventure Works** cubo.  
  
```  
WITH MEMBER [Date].[Calendar].[First2MonthsSecondSemester2003] AS  
    Aggregate(  
        QTD([Date].[Calendar].[Month].[August 2003])  
    )  
SELECT   
    [Date].[Calendar].[First2MonthsSecondSemester2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
