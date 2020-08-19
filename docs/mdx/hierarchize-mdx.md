---
description: Hierarquize (MDX)
title: Hierarquia (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3c1683819420d150e2f9b330ba94bc9e228d167f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429908"
---
# <a name="hierarchize-mdx"></a>Hierarquize (MDX)


  Ordena os membros de um conjunto em uma hierarquia.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Hierarchize(Set_Expression [ , POST ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
## <a name="remarks"></a>Comentários  
 A função de **hierarquia** organiza os membros do conjunto especificado em ordem hierárquica. A função sempre retém duplicatas.  
  
-   Se **post** não for especificado, a função classificará Membros em um nível em sua ordem natural. Sua ordem natural é a ordem padrão dos membros na hierarquia quando nenhuma outra condição de classificação for especificada. Os membros filho seguem imediatamente seus membros pai.  
  
-   Se **post** for especificado, a função de **hierarquia** classificará os membros em um nível usando uma ordem de pós-compilação. Em outras palavras, os membros filho precedem seus pais.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir faz drill up do membro Canadá. A função de **hierarquia** é usada para organizar os membros do conjunto especificado na ordem hierárquica, o que é exigido pela função **DrillupMember** .  
  
```  
SELECT DrillUpMember   
   (  
      Hierarchize  
         (  
            {[Geography].[Geography].[Country].[Canada]  
            ,[Geography].[Geography].[Country].[United States]  
            ,[Geography].[Geography].[State-Province].[Alberta]  
            ,[Geography].[Geography].[State-Province].[Brunswick]  
            ,[Geography].[Geography].[State-Province].[Colorado]   
            }  
         ), {[Geography].[Geography].[Country].[United States]}  
   )  
ON 0  
FROM [Adventure Works]  
```  
  
 O exemplo a seguir retorna a soma do `Measures.[Order Quantity]` membro, agregados nos primeiros nove meses de 2003 contidos na `Date` dimensão, do cubo **Adventure Works** . A função **PeriodsToDate** define as tuplas no conjunto sobre o qual a função de agregação Opera. A função de **hierarquia** organiza os membros do conjunto de membros especificado da dimensão Produto na ordem hierárquica.  
  
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
  
  
