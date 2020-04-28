---
title: Filtro (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3a70bceed4cdccf6a22f0cfea4e5093634f88f1f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68132688"
---
# <a name="filter-mdx"></a>Filter (MDX)


  Retorna o conjunto resultante da filtragem de um conjunto especificado com base em um critério de pesquisa.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Filter(Set_Expression, Logical_Expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Logical_Expression*  
 Uma expressão lógica MDX válida avaliada como verdadeira ou falsa.  
  
## <a name="remarks"></a>Comentários  
 A função **Filter** avalia a expressão lógica especificada em relação a cada tupla no conjunto especificado. A função retorna um conjunto que consiste em cada tupla no conjunto especificado onde a expressão lógica é avaliada como **true**. Se nenhuma tupla for avaliada como **true**, um conjunto vazio será retornado.  
  
 A função **Filter** funciona de maneira semelhante à da função [IIF](../mdx/iif-mdx.md) . A função **IIF** retorna apenas uma das duas opções com base na avaliação de uma expressão lógica MDX, enquanto a função **Filter** retorna um conjunto de tuplas que atendem ao critério de pesquisa especificado. Na verdade, a função de **filtro** é `IIf(Logical_Expression, Set_Expression.Current, NULL)` executada em cada tupla no conjunto e retorna o conjunto resultante.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra o uso da função Filter no eixo Linhas de uma consulta para retornar somente as Datas em que o Valor das Vendas pela Internet é maior do que US$ 10.000:  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `FILTER(`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `,  [Measures].[Internet Sales Amount]>10000)`  
  
 `ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 A função Filter também pode ser usada em definições de membro calculado. O exemplo a seguir retorna a soma do `Measures.[Order Quantity]` membro, agregados nos primeiros nove meses de 2003 contidos na `Date` dimensão, do cubo **Adventure Works** . A função **PeriodsToDate** define as tuplas no conjunto sobre o qual a função de **agregação** Opera. A função de **filtro** limita as tuplas que estão sendo retornadas para aquelas com valores mais baixos para a medida do valor de vendas do revendedor para o período de tempo anterior.  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS Count  
   (Filter  
      (Existing  
         (Reseller.Reseller.Reseller),   
            [Measures].[Reseller Sales Amount] <   
               ([Measures].[Reseller Sales Amount],[Date].Calendar.PrevMember)  
        )  
    )  
MEMBER [Geography].[State-Province].x AS Aggregate   
( {[Geography].[State-Province].&[WA]&[US],   
   [Geography].[State-Province].&[OR]&[US] }   
)  
SELECT NON EMPTY HIERARCHIZE   
   (AddCalculatedMembers   
      ({DrillDownLevel  
         ({[Product].[All Products]})}  
        )  
    ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,   
   [Date].[Calendar].[Calendar Quarter].&[2003]&[4],  
   [Measures].[Declining Reseller Sales])  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
