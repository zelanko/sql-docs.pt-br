---
title: Função Covariance (MDX) | Microsoft Docs
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
- COVARIANCE
dev_langs:
- kbMDX
helpviewer_keywords:
- Covariance function
ms.assetid: 5faf6742-62db-4c5c-8797-096bf1cab273
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: e913d7b925f026aa44b60f3ffe43b9e0fdb735b8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="covariance-mdx"></a>Função Covariance (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna a covariância de população dos pares x-y de valores avaliados em um conjunto, usando a fórmula de população polarizada (dividindo pelo número de pares x-y).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Covariance(Set_Expression,Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Numeric_Expression_y*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número que representa valores do eixo y.  
  
 *Numeric_Expression_x*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número que representa valores do eixo x.  
  
## <a name="remarks"></a>Remarks  
 O **covariância** função avalia o conjunto especificado em relação à primeira expressão numérica, para obter os valores para o eixo y. Em seguida, a função avalia o conjunto especificado em relação à segunda expressão numérica, se especificada, para obter o conjunto de valores para o eixo x. O segundo expressionis numéricos se não for especificado, a função usa o contexto atual das células no conjunto especificado como valores para o eixo x.  
  
 O **covariância** função usa a fórmula de população polarizada. Isso é, em comparação com o [CovarianceN](../mdx/covariancen-mdx.md) função que usa a fórmula de população não polarizada (dividindo pelo número de pares x-y e subtraindo 1).  
  
> [!NOTE]  
>  O **covariância** função ignora células vazias ou células que contêm texto ou valores lógicos são ignorados. Porém, a função contém células com valores zero.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como usar a função de covariância:  
  
```  
WITH   
MEMBER [Measures].[CovarianceDemo] AS  
COVARIANCE([Date].[Date].[Date].Members, [Measures].[Internet Sales Amount], [Measures].[Internet Order Count])   
SELECT {[Measures].[CovarianceDemo]} ON 0   
FROM  
[Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
