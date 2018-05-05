---
title: VarP (MDX) | Microsoft Docs
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
- VARP
dev_langs:
- kbMDX
helpviewer_keywords:
- VarP function [MDX]
ms.assetid: feca648d-bbc8-44c8-9a0e-38f66d914c72
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 5a2d398d7ab26256b7e81e7489676fa4f4beb8e3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="varp-mdx"></a>VarP (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna a variância da população de uma expressão numérica avaliada em um conjunto, usando a fórmula de população polarizada (dividindo por *n*-1).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
VarP(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Numeric_Expression*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número.  
  
## <a name="remarks"></a>Remarks  
 O **VarP** função retorna a variância polarizada de uma expressão numérica especificada avaliada em um conjunto especificado.  
  
 O **VarP** função usa a população polarizada fórmulas, enquanto o [Var](../mdx/var-mdx.md) função usa a fórmula de população não polarizada.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
