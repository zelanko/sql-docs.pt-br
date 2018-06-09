---
title: LinRegSlope (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: aa1c24076f76c4f61692deac69741d8cf1557462
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34741535"
---
# <a name="linregslope-mdx"></a>LinRegSlope (MDX)


  Calcula a regressão linear de um conjunto e retorna o valor do declive na linha de regressão, y = ax + b.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
LinRegSlope(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Numeric_Expression_y*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número que representa valores do eixo y.  
  
 *Numeric_Expression_x*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número que representa valores do eixo x.  
  
## <a name="remarks"></a>Remarks  
 A regressão linear, que usa o método dos mínimos quadrados, calcula a equação de uma linha de regressão (ou seja, a linha mais adequada para uma série de pontos). A linha de regressão tem a seguinte equação, onde um é a inclinação e b é a interceptação:  
  
 y = ax+b  
  
 O **LinRegSlope** função avalia o conjunto especificado em relação a primeira expressão numérica para obter os valores para o eixo y. Em seguida, a função avalia a expressão do conjunto especificado em relação à segunda expressão numérica, se especificada, para obter os valores para o eixo x. Se a segunda expressão numérica não for especificada, a função utilizará o contexto atual das células no conjunto especificado como os valores para o eixo x. A não especificação do argumento de eixo x geralmente é usada com a dimensão Tempo.  
  
 Depois de obter o conjunto de pontos, o **LinRegSlope** função retorna o declive da linha de regressão (na equação anterior).  
  
> [!NOTE]  
>  O **LinRegSlope** função ignora células vazias ou células que contêm texto ou valores lógicos. Porém, a função contém células com valores zero.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o declive de uma linha de regressão para as medidas de vendas de unidade e vendas na loja.  
  
```  
LinRegSlope(LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
