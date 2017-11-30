---
title: "Função Parent (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: PARENT
dev_langs: kbMDX
helpviewer_keywords: Parent function
ms.assetid: 7be9b172-4241-4618-bdba-53cde8badd9b
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 083babb3b0c87e03b1605527b85dc3e835127d05
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
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
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
