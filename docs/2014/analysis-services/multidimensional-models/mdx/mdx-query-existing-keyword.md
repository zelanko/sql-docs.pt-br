---
title: Palavra-chave EXISTING (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- EXISTING
helpviewer_keywords:
- Existing keyword
ms.assetid: 651ee9ac-04ef-4316-87c9-a3df5ac27d22
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a781fb58f45c478b6a3611132a210b14012ffb72
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37228386"
---
# <a name="existing-keyword-mdx"></a>Palavra-chave EXISTING (MDX)
  Força a avaliação de um conjunto especificado no contexto atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Existing Set_Expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão de conjunto de expressões multidimensionais (MDX) válida.  
  
## <a name="remarks"></a>Remarks  
 Por padrão, são avaliados conjuntos no contexto do cubo que contém os membros do conjunto. O `Existing` força a palavra-chave a ser avaliada dentro do contexto atual em vez disso, um conjunto especificado.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna a contagem dos revendedores cujas vendas caíram ao longo do período anterior, com base em valores de Estado do membro, selecionados pelo usuário, avaliados usando a função `Aggregate`. A palavra-chave [Hierarchize &#40;MDX&#41;](/sql/mdx/hierarchize-mdx) e [DrilldownLevel (MDX)](/sql/mdx/drilldownlevel-mdx) são usadas para retornar valores por queda de vendas por categorias de produto na dimensão Produto. O `Existing` forças de palavra-chave a set no `Filter` função a ser avaliada no contexto atual, ou seja, para os membros Washington e Oregon da hierarquia de atributo estado-província.  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS  
   Count  
      (Filter  
         (Existing  
            (Reseller.Reseller.Reseller)  
         , [Measures].[Reseller Sales Amount] <   
            ([Measures].[Reseller Sales Amount]  
               ,[Date].Calendar.PrevMember  
            )  
        )  
      )  
MEMBER [Geography].[State-Province].x AS   
   Aggregate   
      ( {[Geography].[State-Province].&[WA]&[US]  
         , [Geography].[State-Province].&[OR]&[US] }   
      )  
SELECT NON EMPTY HIERARCHIZE   
      (AddCalculatedMembers   
         (   
            {DrillDownLevel  
               ({[Product].[All Products]}  
               )  
            }   
         )   
      ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE   
      ( [Geography].[State-Province].x  
        , [Date].[Calendar].[Calendar Quarter].&[2003]&[4]  
        ,[Measures].[Declining Reseller Sales]  
      )  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Contagem de &#40;definir&#41; &#40;MDX&#41;](/sql/mdx/count-set-mdx)   
 [AddCalculatedMembers &#40;MDX&#41;](/sql/mdx/addcalculatedmembers-mdx)   
 [Agregação &#40;MDX&#41;](/sql/mdx/aggregate-mdx)   
 [Filtro &#40;MDX&#41;](/sql/mdx/filter-mdx)   
 [Propriedades &#40;MDX&#41;](/sql/mdx/properties-mdx)   
 [DrilldownLevel &#40;MDX&#41;](/sql/mdx/drilldownlevel-mdx)   
 [Hierarquize &#40;MDX&#41;](/sql/mdx/hierarchize-mdx)   
 [Referência da função MDX &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx)  
  
  
