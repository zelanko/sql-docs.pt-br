---
title: Palavra-chave EXISTING (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- EXISTING
helpviewer_keywords:
- Existing keyword
ms.assetid: 651ee9ac-04ef-4316-87c9-a3df5ac27d22
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: c3a9ebbb73e8bf2b305a7ab2730439ffd0d53f8f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-query---existing-keyword"></a>Consulta MDX - palavra-chave existente
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Força a ser avaliada no contexto atual um conjunto especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Existing Set_Expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão de conjunto de expressões multidimensionais (MDX) válida.  
  
## <a name="remarks"></a>Remarks  
 Por padrão, são avaliados conjuntos no contexto do cubo que contém os membros do conjunto. A palavra-chave **Existing** força a avaliação de um conjunto especificado no contexto atual.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna a contagem dos revendedores cujas vendas caíram ao longo do período anterior, com base em valores de Estado do membro, selecionados pelo usuário, avaliados usando a função **Aggregate** . A palavra-chave [Hierarchize &#40;MDX&#41;](../../../mdx/hierarchize-mdx.md) e [DrilldownLevel (MDX)](../../../mdx/drilldownlevel-mdx.md) são usadas para retornar valores por queda de vendas por categorias de produto na dimensão Produto. A palavra-chave **Existing** força a avaliação do conjunto na função **Filter** no contexto atual, ou seja, para os membros Washington e Oregon da hierarquia de atributo Estado.  
  
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
 [Count &#40;Set&#41; &#40;MDX&#41;](../../../mdx/count-set-mdx.md)   
 [AddCalculatedMembers &#40; MDX &#41;](../../../mdx/addcalculatedmembers-mdx.md)   
 [Agregação &#40; MDX &#41;](../../../mdx/aggregate-mdx.md)   
 [Filtro &#40; MDX &#41;](../../../mdx/filter-mdx.md)   
 [Propriedades &#40; MDX &#41;](../../../mdx/properties-mdx.md)   
 [DrilldownLevel &#40; MDX &#41;](../../../mdx/drilldownlevel-mdx.md)   
 [Hierarquize &#40; MDX &#41;](../../../mdx/hierarchize-mdx.md)   
 [Referência de função MDX &#40; MDX &#41;](../../../mdx/mdx-function-reference-mdx.md)  
  
  
