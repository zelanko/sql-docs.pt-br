---
title: CovarianceN (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 796dc37127eba984477aef628e4ae9161db4637e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68047184"
---
# <a name="covariancen-mdx"></a>CovarianceN (MDX)


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
  
## <a name="remarks"></a>Comentários  
 O **CovarianceN** função avalia o conjunto especificado em relação a primeira expressão numérica, para obter os valores para o eixo y. Em seguida, a função avalia o conjunto especificado em relação à segunda expressão numérica, se especificada, para obter o conjunto de valores para o eixo x. Se a segunda expressão numérica não for especificada, a função utilizará o contexto atual das células no conjunto especificado como valores para o eixo x.  
  
 O **CovarianceN** função usa a fórmula de população não polarizada. Isso está em contraste com o [covariância](../mdx/covariance-mdx.md) função que usa a fórmula de população polarizada (dividindo pelo número de pares x-y).  
  
> [!NOTE]  
>  O **CovarianceN** função ignora células vazias ou células que contêm texto ou valores lógicos. Porém, a função contém células com valores zero.  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
