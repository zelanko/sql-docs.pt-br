---
title: Função cousin (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8a98d496467e2fd75924b0067257f192c79cdf6e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68047253"
---
# <a name="cousin-mdx"></a>Função Cousin (MDX)


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
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
