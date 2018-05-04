---
title: FirstSibling (MDX) | Microsoft Docs
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
- FIRSTSIBLING
dev_langs:
- kbMDX
helpviewer_keywords:
- FirstSibling function
ms.assetid: ed2fbd36-6665-4445-a894-cbeca29584ab
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: c753156143c505c4782c3cd43256902a2addc728
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="firstsibling-mdx"></a>FirstSibling (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
