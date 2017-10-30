---
title: Hierarquize (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- HIERARCHIZE
dev_langs:
- kbMDX
helpviewer_keywords:
- Hierarchize function
ms.assetid: e9795003-70e7-4b4c-9074-45b5b9b817fa
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d0c093d032b587a8935d12c8234ab33da52ee86d
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="hierarchize-mdx"></a>Hierarquize (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ordena os membros de um conjunto em uma hierarquia.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Hierarchize(Set_Expression [ , POST ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
## <a name="remarks"></a>Comentários  
 O **Hierarchize** função organiza os membros do conjunto especificado em ordem hierárquica. A função sempre retém duplicatas.  
  
-   Se **POST** não for especificado, a função classificará os membros em um nível em sua ordem natural. Sua ordem natural é a ordem padrão dos membros na hierarquia quando nenhuma outra condição de classificação for especificada. Os membros filho seguem imediatamente seus membros pai.  
  
-   Se **POST** for especificado, o **Hierarchize** função classifica os membros em um nível usando uma ordem pós-natural. Em outras palavras, os membros filho precedem seus pais.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir faz drill up do membro Canadá. O **Hierarchize** função é usada para organizar os membros do conjunto especificado em ordem hierárquica, que é necessária a **DrillUpMember** função.  
  
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
  
 O exemplo a seguir retorna a soma da `Measures.[Order Quantity]` membro, agregado sobre os primeiros nove meses do ano calendário 2003 contidos no `Date` dimensão, do **Adventure Works** cubo. O **PeriodsToDate** função define as tuplas no conjunto sobre o qual a função Aggregate opera. O **Hierarchize** função organiza os membros do conjunto especificado de membros da dimensão de produto na ordem hierárquica.  
  
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
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

