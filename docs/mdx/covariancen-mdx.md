---
title: CovarianceN (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- COVARIANCEN
dev_langs:
- kbMDX
helpviewer_keywords:
- Covariancen function
ms.assetid: 1cc621cd-ffa0-40aa-91f0-bc5cb57f692b
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 35bf5e9917545fc7bcc1fac6ae3aae2d289c65fc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="covariancen-mdx"></a>CovarianceN (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna a covariância de exemplo dos pares x-y de valores avaliados em um conjunto, usando a fórmula de população não polarizada (dividindo pelo número de pares x-y).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CovarianceN(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Numeric_Expression_y*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número que representa valores do eixo y.  
  
 *Numeric_Expression_x*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número que representa valores do eixo x.  
  
## <a name="remarks"></a>Remarks  
 O **CovarianceN** função avalia o conjunto especificado em relação à primeira expressão numérica, para obter os valores para o eixo y. Em seguida, a função avalia o conjunto especificado em relação à segunda expressão numérica, se especificada, para obter o conjunto de valores para o eixo x. Se a segunda expressão numérica não for especificada, a função utilizará o contexto atual das células no conjunto especificado como valores para o eixo x.  
  
 O **CovarianceN** função usa a fórmula de população não polarizada. Isso é, em comparação com o [covariância](../mdx/covariance-mdx.md) função que usa a fórmula de população polarizada (dividindo pelo número de pares x-y).  
  
> [!NOTE]  
>  O **CovarianceN** função ignora células vazias ou células que contêm texto ou valores lógicos. Porém, a função contém células com valores zero.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
