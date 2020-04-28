---
title: Contagem (definida) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: aac2f72cc8cd91e1964fd7734b858be8215cfdd8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68047288"
---
# <a name="count-set-mdx"></a>Count (Conjunto) (MDX)


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
  
## <a name="remarks"></a>Comentários  
 A função **Count (Set)** inclui ou exclui células vazias, dependendo da sintaxe usada. Se a sintaxe padrão for usada, as células vazias poderão ser excluídas ou incluídas usando os sinalizadores **EXCLUDEEMPTY** ou **INCLUDEEMPTY** , respectivamente. Se a sintaxe alternativa for usada, a função sempre incluirá células vazias.  
  
 Para excluir células vazias na contagem de um conjunto, use a sintaxe padrão e o sinalizador **EXCLUDEEMPTY** opcional.  
  
> [!NOTE]  
>  A função **Count (Set)** conta as células vazias por padrão. Por outro lado, a função **Count** em OLE DB que conta um conjunto exclui células vazias por padrão.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir conta o número de células no conjunto de membros que consistem nos filhos da hierarquia de atributo Nome do Modelo na dimensão Produto.  
  
```  
WITH MEMBER measures.X AS  
   [Product].[Model Name].children.count   
SELECT Measures.X ON 0  
FROM [Adventure Works]  
```  
  
 O exemplo a seguir conta o número de produtos na dimensão produto usando a função **DrilldownLevel** em conjunto com a função **Count** .  
  
```  
Count(DrilldownLevel (   
   [Product].[Product].[Product]))  
```  
  
 O exemplo a seguir retorna esses revendedores com vendas decrescentes em comparação com o trimestre do calendário anterior, usando a função **Count** em conjunto com a função **Filter** e uma série de outras funções. Essa consulta usa a função de **agregação** para dar suporte à seleção de vários membros de Geografia, como para seleção de dentro de uma lista suspensa em um aplicativo cliente.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Contagem de &#40;de dimensões&#41; &#40;MDX&#41;](../mdx/count-dimension-mdx.md)   
 [Contar &#40;níveis de hierarquia&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Contar &#40;tupla&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [DrilldownLevel&#41;MDX &#40;](../mdx/drilldownlevel-mdx.md)   
 [AddCalculatedMembers&#41;MDX &#40;](../mdx/addcalculatedmembers-mdx.md)   
 [Hierarquiar &#40;&#41;MDX](../mdx/hierarchize-mdx.md)   
 [Propriedades &#40;MDX&#41;](../mdx/properties-mdx.md)   
 [&#41;&#40;MDX de agregação](../mdx/aggregate-mdx.md)   
 [Filtrar &#40;&#41;MDX](../mdx/filter-mdx.md)   
 [PrevMember&#41;MDX &#40;](../mdx/prevmember-mdx.md)   
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
