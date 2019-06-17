---
title: LinRegVariance (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b3ae56238623c41d29ccb388a5aaa178352af196
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63208744"
---
# <a name="linregvariance-mdx"></a>LinRegVariance (MDX)


  Calcula a regressão linear de um conjunto e retorna a variância associada à linha de regressão, y = ax + b.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
LinRegVariance(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Numeric_Expression_y*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número que representa valores do eixo y.  
  
 *Numeric_Expression_x*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número que representa valores do eixo x.  
  
## <a name="remarks"></a>Comentários  
 A regressão linear, que usa o método dos mínimos quadrados, calcula a equação de uma linha de regressão (ou seja, a linha mais adequada para uma série de pontos). A linha de regressão tem a seguinte equação, em que um é a inclinação e b é a interceptação:  
  
 y = ax+b  
  
 O **LinRegVariance** função avalia o setagainst especificado, a primeira expressão numérica para obter os valores para o eixo y. A função, em seguida, avalia a expressão numérica em segundo lugar, de setagainst especificado se especificado, para obter os valores para o eixo x. O segundo expressionis numéricos se não for especificado, a função usa o contexto atual das células no conjunto especificado como os valores para o eixo x. A não especificação do argumento de eixo x geralmente é usada com a dimensão Tempo.  
  
 Depois de obter o conjunto de pontos, o **LinRegVariance** função retorna a variância estatística que descreve o ajuste da equação linear aos pontos.  
  
> [!NOTE]  
>  O **LinRegVariance** função ignora células vazias ou células que contêm texto ou valores lógicos. Porém, a função contém células com valores zero.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna a variância estatística que descreve o ajuste da equação linear aos pontos para as medidas de vendas de unidade e vendas na loja.  
  
```  
LinRegVariance(LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
