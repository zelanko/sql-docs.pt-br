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
manager: kfile
ms.openlocfilehash: d740148052712a69a39e0de314496733b3b26a8b
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34740525"
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
  
## <a name="remarks"></a>Remarks  
 O **filtro** função avalia a expressão lógica especificada em relação a cada tupla no conjunto especificado. A função retorna um conjunto que consiste em cada tupla no conjunto especificado em que a expressão lógica é avaliada como **true**. Se nenhuma tupla for avaliada como **true**, um conjunto vazio será retornado.  
  
 O **filtro** função funciona de maneira semelhante do [IIf](../mdx/iif-mdx.md) função. O **IIf** função retorna apenas uma das duas opções com base na avaliação de uma expressão lógica MDX, enquanto o **filtro** função retorna um conjunto de tuplas que atendem à condição de pesquisa especificada. Na verdade, o **filtro** função executa `IIf(Logical_Expression, Set_Expression.Current, NULL)` em cada tupla no conjunto e retorna o conjunto resultante.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra o uso da função Filter no eixo Linhas de uma consulta para retornar somente as Datas em que o Valor das Vendas pela Internet é maior do que US$ 10.000:  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `FILTER(`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `,  [Measures].[Internet Sales Amount]>10000)`  
  
 `ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 A função Filter também pode ser usada em definições de membro calculado. O exemplo a seguir retorna a soma da `Measures.[Order Quantity]` membro, agregado sobre os primeiros nove meses do ano calendário 2003 contidos no `Date` dimensão, do **Adventure Works** cubo. O **PeriodsToDate** função define as tuplas no conjunto sobre o qual o **agregação** função opera. O **filtro** função limita as tuplas sejam retornadas para aquelas com valores mais baixos para a medida quantidade de vendas de revendedor para o período de tempo anterior.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
