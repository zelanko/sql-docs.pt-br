---
title: FirstSibling (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 671dd0b2b400362fe3a2274c4687f93192f04da4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68105456"
---
# <a name="firstsibling-mdx"></a>FirstSibling (MDX)


  Retorna o primeiro filho do pai de um membro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Member_Expression.FirstSibling   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
### <a name="example"></a>Exemplo  
 A consulta a seguir retorna o primeiro irmão do ano fiscal 2003 na hierarquia Ano fiscal, que é o Ano fiscal 2002.  
  
```  
SELECT [Date].[Fiscal].[Fiscal Year].&[2003].FirstSibling ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
