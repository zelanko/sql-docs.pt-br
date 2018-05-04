---
title: StdevP (MDX) | Microsoft Docs
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
- STDEVP
dev_langs:
- kbMDX
helpviewer_keywords:
- StdevP function [MDX]
ms.assetid: cd8ae7c9-3cef-49f0-bb41-8f577c7b6f31
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 617cd92b6728aa19fbb6599f71fab5374a331857
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="stdevp-mdx"></a>StdevP (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o desvio padrão da população de uma expressão numérica avaliada em um conjunto, usando a fórmula de população polarizada (dividindo por *n*).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
StdevP(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Numeric_Expression*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número.  
  
## <a name="remarks"></a>Remarks  
 O **StdevP** função usa a população polarizada fórmulas, enquanto o [Stdev](../mdx/stdev-mdx.md) função usa a fórmula de população não polarizada.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o desvio padrão para Quantidade de Pedidos pela Internet, avaliado em relação aos três primeiros meses do ano calendário 2003, usando a fórmula de população polarizada.  
  
```  
WITH MEMBER Measures.x AS   
   StdevP   
   ( { [Date].[Calendar].[Month].[January 2003],  
       [Date].[Calendar].[Month].[February 2003],  
       [Date].[Calendar].[Month].[March 2003]},  
    [Measures].[Internet Order Quantity])  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
