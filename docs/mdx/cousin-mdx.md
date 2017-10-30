---
title: "Função cousin (MDX) | Microsoft Docs"
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
- COUSIN
dev_langs:
- kbMDX
helpviewer_keywords:
- Cousin function
ms.assetid: 9a416685-d35d-4d9c-a9f6-4574cbe59aea
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8f8e73b19a5c2253275852e38988f1a85a5c9472
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="cousin-mdx"></a>Função Cousin (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o membro filho com a mesma posição relativa sob um membro pai como o membro filho especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Cousin( Member_Expression , Ancestor_Member_Expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
 *Ancestor_Member_Expression*  
 Uma linguagem de membro MDX válida que retorna um membro ancestral.  
  
## <a name="remarks"></a>Comentários  
 Esta função afeta a ordem e a posição dos membros nos níveis. Se duas hierarquias existirem, na qual a primeira tem quatro níveis e a segunda tem cinco níveis, o primo do terceiro nível da primeira hierarquia será o terceiro nível da segunda hierarquia.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir recupera o primo do quarto trimestre do ano fiscal de 2002, com base no ancestral do nível do ano fiscal de 2003. O primo recuperado é o quarto trimestre do ano fiscal de 2003.  
  
```  
SELECT Cousin   
   ( [Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002],  
     [Date].[Fiscal].[FY 2003]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
 O exemplo a seguir recupera o primo do mês de julho do ano fiscal de 2002, com base no ancestral do nível do trimestre no segundo trimestre do ano fiscal de 2004. O primo recuperado é o mês de outubro de 2003.  
  
```  
SELECT Cousin   
   ([Date].[Fiscal].[Month].[July 2002] ,  
    [Date].[Fiscal].[Fiscal Quarter].[Q2 FY 2004]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

