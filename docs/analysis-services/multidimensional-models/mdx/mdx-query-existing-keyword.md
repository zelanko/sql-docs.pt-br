---
title: Palavra-chave EXISTING (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d41b49e4585d2a256250a009b09ffa9ed94ea925
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208727"
---
# <a name="mdx-query---existing-keyword"></a>Consulta MDX – Palavra-chave EXISTING
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Força a avaliação de um conjunto especificado no contexto atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Existing Set_Expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão de conjunto de expressões multidimensionais (MDX) válida.  
  
## <a name="remarks"></a>Comentários  
 Por padrão, são avaliados conjuntos no contexto do cubo que contém os membros do conjunto. A palavra-chave **Existing** força a avaliação de um conjunto especificado no contexto atual.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna a contagem dos revendedores cujas vendas caíram ao longo do período anterior, com base em valores de Estado do membro, selecionados pelo usuário, avaliados usando a função **Aggregate** . A palavra-chave [Hierarchize &#40;MDX&#41;](../../../mdx/hierarchize-mdx.md) e [DrilldownLevel (MDX)](../../../mdx/drilldownlevel-mdx.md) são usadas para retornar valores por queda de vendas por categorias de produto na dimensão Produto. O **Existing** força a palavra-chave set na **filtro** função a ser avaliada no contexto atual, ou seja, para os membros Washington e Oregon da hierarquia de atributo estado-província.  
  
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
 [Count &#40;Set&#41; &#40;MDX&#41;](../../../mdx/count-set-mdx.md)   
 [AddCalculatedMembers &#40;MDX&#41;](../../../mdx/addcalculatedmembers-mdx.md)   
 [Aggregate &#40;MDX&#41;](../../../mdx/aggregate-mdx.md)   
 [Filter &#40;MDX&#41;](../../../mdx/filter-mdx.md)   
 [Properties &#40;MDX&#41;](../../../mdx/properties-mdx.md)   
 [DrilldownLevel &#40;MDX&#41;](../../../mdx/drilldownlevel-mdx.md)   
 [Hierarchize &#40;MDX&#41;](../../../mdx/hierarchize-mdx.md)   
 [Referência da Função MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)  
  
  
