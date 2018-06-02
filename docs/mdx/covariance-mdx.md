---
title: Função Covariance (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 06b86c47b5da75c44d528f77a60e8168fd8b2260
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34577878"
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
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
