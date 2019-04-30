---
title: Lastsibling=2==retorna (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a762fe474be4bd7337b8608af2c6aabcb6a34fd8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63270507"
---
# <a name="lastsibling-mdx"></a>LastSibling (MDX)


  Retorna o último filho do pai de um membro especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Member_Expression.LastSibling   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir retorna a medida padrão para o último dia de julho de 2002.  
  
```  
SELECT [Date].[Fiscal].[Date].&[20020717].LastSibling   
   ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
