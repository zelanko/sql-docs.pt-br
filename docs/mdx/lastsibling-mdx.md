---
title: LastSibling (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 281d8a76ba66a6615eab44e8f22225e417bff31e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905806"
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
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
