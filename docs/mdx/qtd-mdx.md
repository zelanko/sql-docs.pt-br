---
title: Qtd (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7a8856b28d8eec76d2bc262c4209b007c0a7fa04
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68020642"
---
# <a name="qtd-mdx"></a>Qtd (MDX)


  Retorna um conjunto de membros irmãos do mesmo nível de um determinado membro, começando com o primeiro irmão e terminando com o membro determinado, como restrito pelo nível de *trimestre* na dimensão de tempo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Qtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Comentários  
 Se uma expressão de membro não for especificada, o padrão será o membro atual da primeira hierarquia com um nível do tipo *trimestres* na primeira dimensão do tipo *time* no grupo de medidas.  
  
 A função **Qtd** é uma função de atalho para o [PeriodsToDate &#40;MDX&#41;](../mdx/periodstodate-mdx.md) função cujo argumento de expressão de nível é definido como *trimestre*. Ou seja, `Qtd(Member_Expression)` é funcionalmente equivalente a `PeriodsToDate(Quarter_Level_Expression, Member_Expression)`.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna a soma do `Measures.[Order Quantity]` membro, agregados nos primeiros dois meses do terceiro trimestre do ano civil 2003 que estão contidos na `Date` dimensão, do cubo **Adventure Works** .  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
