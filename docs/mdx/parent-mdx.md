---
title: Função Parent (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9449c81e9f8e8de0c21d96062337e91b2f56398d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037189"
---
# <a name="parent-mdx"></a>Função Parent (MDX)


  Retorna o pai de um membro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Member_Expression.Parent   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Comentários  
 O **pai** função retorna o membro pai do membro especificado.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir retornam o pai do membro 1º de julho de 2001. O primeiro exemplo especifica esse membro no contexto da hierarquia de atributo Data e retorna o membro Todos os Períodos.  
  
```  
SELECT [Date].[Date].[July 1, 2001].Parent ON 0  
FROM [Adventure Works]  
```  
  
 O exemplo a seguir especifica o membro 1º de julho de 2001 no contexto da hierarquia Calendário.  
  
```  
SELECT [Date].[Calendar].[July 1, 2001].Parent ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
