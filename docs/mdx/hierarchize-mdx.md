---
title: Hierarquize (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8ab2c866f201c53684c316282a143b4f672cb8e9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105429"
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
 O **Hierarchize** função organiza os membros do conjunto especificado em ordem hierárquica. A função sempre retém duplicatas.  
  
-   Se **POST** não for especificado, a função classificará os membros em um nível na ordem natural. Sua ordem natural é a ordem padrão dos membros na hierarquia quando nenhuma outra condição de classificação for especificada. Os membros filho seguem imediatamente seus membros pai.  
  
-   Se **POST** for especificado, o **Hierarchize** função classifica os membros em um nível usando a ordem pós-natural. Em outras palavras, os membros filho precedem seus pais.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir faz drill up do membro Canadá. O **Hierarchize** função é usada para organizar os membros do conjunto especificado em ordem hierárquica, que é necessário para o **DrillUpMember** função.  
  
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
  
 O exemplo a seguir retorna a soma do `Measures.[Order Quantity]` membro, agregado sobre os primeiros nove meses de 2003 contidos na `Date` dimensão, da **Adventure Works** cubo. O **PeriodsToDate** função define as tuplas no conjunto sobre o qual a função Aggregate opera. O **Hierarchize** função organiza os membros do conjunto especificado de membros da dimensão de produto na ordem hierárquica.  
  
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
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
