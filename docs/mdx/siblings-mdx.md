---
title: Irmãos (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SIBLINGS
dev_langs:
- kbMDX
helpviewer_keywords:
- Siblings function
ms.assetid: 33e63808-f07e-44f7-8dfa-4dd9fd89ec82
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: c7eee2d7b0e0f6118103f62687eac40c4d7882bb
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="siblings-mdx"></a>Siblings (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna os irmãos de um membro especificado, inclusive o próprio membro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Member_Expression.Siblings   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir retorna a medida padrão para os irmãos de março de 2003, que são janeiro e fevereiro de 2003, incluindo março de 2003.  
  
```  
SELECT [Date].[Calendar].[Month].[March 2003].Siblings ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
