---
title: "Palavra-chave EXISTING (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "EXISTING"
helpviewer_keywords: 
  - "palavra-chave existente"
ms.assetid: 651ee9ac-04ef-4316-87c9-a3df5ac27d22
caps.latest.revision: 38
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Palavra-chave EXISTING (MDX)
  Força a avaliação de um conjunto especificado no contexto atual.  
  
## Sintaxe  
  
```  
  
Existing Set_Expression  
```  
  
## Argumentos  
 *Set_Expression*  
 Uma expressão de conjunto de expressões multidimensionais (MDX) válida.  
  
## Comentários  
 Por padrão, são avaliados conjuntos no contexto do cubo que contém os membros do conjunto. A palavra-chave **Existing** força a avaliação de um conjunto especificado no contexto atual.  
  
## Exemplo  
 O exemplo a seguir retorna a contagem dos revendedores cujas vendas caíram ao longo do período anterior, com base em valores de Estado do membro, selecionados pelo usuário, avaliados usando a função **Aggregate**. As funções [Hierarquize &#40;MDX&#41;](../../../mdx/hierarchize-mdx.md) e [DrilldownLevel (MDX)](../../../mdx/drilldownlevel-mdx.md) são usadas para retornar valores por queda de vendas por categorias de produto na dimensão Produto. A palavra-chave **Existing** força a avaliação do conjunto na função **Filter** no contexto atual, ou seja, para os membros Washington e Oregon da hierarquia de atributo Estado.  
  
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
  
## Consulte também  
 [Count &#40;Set&#41; &#40;MDX&#41;](../../../mdx/count-set-mdx.md)   
 [AddCalculatedMembers &#40;MDX&#41;](../../../mdx/addcalculatedmembers-mdx.md)   
 [Aggregate &#40;MDX&#41;](../../../mdx/aggregate-mdx.md)   
 [Filter &#40;MDX&#41;](../../../mdx/filter-mdx.md)   
 [Properties &#40;MDX&#41;](../../../mdx/properties-mdx.md)   
 [DrilldownLevel &#40;MDX&#41;](../../../mdx/drilldownlevel-mdx.md)   
 [Hierarchize &#40;MDX&#41;](../../../mdx/hierarchize-mdx.md)   
 [Referência da Função MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)  
  
  