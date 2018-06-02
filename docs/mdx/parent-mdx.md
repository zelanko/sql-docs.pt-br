---
title: Função Parent (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 32922aebffd9704725e534742656b86348f5e1ee
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580638"
---
# <a name="parent-mdx"></a>Função Parent (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o pai de um membro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Member_Expression.Parent   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Remarks  
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
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
