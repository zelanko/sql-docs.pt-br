---
title: Count (conjunto) (MDX) | Microsoft Docs
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
- COUNT
dev_langs:
- kbMDX
helpviewer_keywords:
- Count function [MDX]
ms.assetid: 22f530e9-f8e1-4608-affa-9a2bc0821591
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 8fb02f59ec89c8c3c54c13973251ebdd78cfa32f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="count-set-mdx"></a>Count (Conjunto) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o número de células em um conjunto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Standard syntax  
Count(Set_Expression [ , ( EXCLUDEEMPTY | INCLUDEEMPTY ) ] )  
  
Alternate syntax  
Set_Expression.Count  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
## <a name="remarks"></a>Remarks  
 O **Count (conjunto)** função inclui ou exclui células vazias, dependendo da sintaxe usada. Se a sintaxe padrão for usada, células vazias podem ser excluídas ou incluídas usando o **EXCLUDEEMPTY** ou **INCLUDEEMPTY** sinalizadores, respectivamente. Se a sintaxe alternativa for usada, a função sempre incluirá células vazias.  
  
 Para excluir células vazias na contagem de um conjunto, use a sintaxe padrão e opcional **EXCLUDEEMPTY** sinalizador.  
  
> [!NOTE]  
>  O **Count (conjunto)** função conta células vazias por padrão. Em contraste, o **contagem** função no OLE DB que conta um conjunto exclui células vazias por padrão.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir conta o número de células no conjunto de membros que consistem nos filhos da hierarquia de atributo Nome do Modelo na dimensão Produto.  
  
```  
WITH MEMBER measures.X AS  
   [Product].[Model Name].children.count   
SELECT Measures.X ON 0  
FROM [Adventure Works]  
```  
  
 O exemplo a seguir conta o número de produtos na dimensão produto usando o **DrilldownLevel** função em conjunto com o **contagem** função.  
  
```  
Count(DrilldownLevel (   
   [Product].[Product].[Product]))  
```  
  
 O exemplo a seguir retorna os revendedores com queda de vendas em comparação ao trimestre do calendário anterior, usando o **contagem** função em conjunto com o **filtro** função e um número de outras funções. Essa consulta usa o **agregação** função para dar suporte a seleção de vários membros de geografia, como a seleção em uma lista suspensa em um aplicativo cliente.  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS  
   Count  
   (Filter  
      (Existing(Reseller.Reseller.Reseller),  
         [Measures].[Reseller Sales Amount]   
         < ([Measures].[Reseller Sales Amount],  
            [Date].Calendar.PrevMember)  
      )  
   )  
MEMBER [Geography].[State-Province].x AS   
   Aggregate  
   ( {[Geography].[State-Province].&[WA]&[US],   
      [Geography].[State-Province].&[OR]&[US] }   
   )  
SELECT NON EMPTY HIERARCHIZE   
   (AddCalculatedMembers   
      ({DrillDownLevel  
         ({[Product].[All Products]})  
      })  
   ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,  
   [Date].[Calendar].[Calendar Quarter].&[2003]&[4]  
   ,[Measures].[Declining Reseller Sales])  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Contagem de &#40;dimensão&#41; &#40;MDX&#41;](../mdx/count-dimension-mdx.md)   
 [Contagem de &#40;níveis de hierarquia&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Contagem de &#40;tupla&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [DrilldownLevel & #40; MDX & #41;](../mdx/drilldownlevel-mdx.md)   
 [AddCalculatedMembers & #40; MDX & #41;](../mdx/addcalculatedmembers-mdx.md)   
 [Hierarquize & #40; MDX & #41;](../mdx/hierarchize-mdx.md)   
 [Propriedades & #40; MDX & #41;](../mdx/properties-mdx.md)   
 [Agregação & #40; MDX & #41;](../mdx/aggregate-mdx.md)   
 [Filtro & #40; MDX & #41;](../mdx/filter-mdx.md)   
 [PrevMember &#40;MDX&#41;](../mdx/prevmember-mdx.md)   
 [Referência de função MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
