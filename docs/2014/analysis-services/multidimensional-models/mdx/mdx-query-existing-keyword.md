---
title: Palavra-chave EXISTing (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- EXISTING
helpviewer_keywords:
- Existing keyword
ms.assetid: 651ee9ac-04ef-4316-87c9-a3df5ac27d22
author: minewiskan
ms.author: owend
ms.openlocfilehash: 115444c832fe8fe9b258a0c23b97b97553f32e8e
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546208"
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
  
## <a name="remarks"></a>Comentários  
 Por padrão, são avaliados conjuntos no contexto do cubo que contém os membros do conjunto. A palavra-chave `Existing` força a avaliação de um conjunto especificado no contexto atual.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna a contagem dos revendedores cujas vendas caíram ao longo do período anterior, com base em valores de Estado do membro, selecionados pelo usuário, avaliados usando a função `Aggregate`. A palavra-chave [Hierarchize &#40;MDX&#41;](/sql/mdx/hierarchize-mdx) e [DrilldownLevel (MDX)](/sql/mdx/drilldownlevel-mdx) são usadas para retornar valores por queda de vendas por categorias de produto na dimensão Produto. A `Existing` palavra-chave força o conjunto na `Filter` função a ser avaliada no contexto atual, ou seja, para os membros Washington e Oregon da hierarquia de atributo State-província.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Contagem &#40;definida&#41; &#40;MDX&#41;](/sql/mdx/count-set-mdx)   
 [AddCalculatedMembers&#41;MDX &#40;](/sql/mdx/addcalculatedmembers-mdx)   
 [&#41;&#40;MDX de agregação](/sql/mdx/aggregate-mdx)   
 [Filtrar &#40;&#41;MDX](/sql/mdx/filter-mdx)   
 [Propriedades &#40;MDX&#41;](/sql/mdx/properties-mdx)   
 [DrilldownLevel&#41;MDX &#40;](/sql/mdx/drilldownlevel-mdx)   
 [Hierarquiar &#40;&#41;MDX](/sql/mdx/hierarchize-mdx)   
 [Referência da Função MDX &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx)  
  
  
