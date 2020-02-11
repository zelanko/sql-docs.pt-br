---
title: LinRegR2 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2e38df1a24b76ee40aae3a5ab3c28dd9bca2b310
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905526"
---
# <a name="linregr2-mdx"></a>LinRegR2 (MDX)


  Calcula a regressão linear de um conjunto e retorna o coeficiente de determinação, R<sup>2</sup>.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
LinRegR2(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Numeric_Expression_y*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número que representa valores do eixo y.  
  
 *Numeric_Expression_x*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número que representa valores do eixo x.  
  
## <a name="remarks"></a>Comentários  
 A regressão linear, que usa o método dos mínimos quadrados, calcula a equação de uma linha de regressão (ou seja, a linha mais adequada para uma série de pontos). A linha de regressão tem a seguinte equação, em que a é a inclinação e b é a interceptação:  
  
 y = ax+b  
  
 A função **LinRegR2** avalia a primeira expressão numérica especificada para obter os valores para o eixo y. Em seguida, a função avalia o conjunto especificado em relação à segunda expressão numérica, se especificada, para obter os valores para o eixo x. Se a segunda expressão numéricanão for especificada, a função usará o contexto atual das células no conjunto especificado como os valores para o eixo x. A não especificação do argumentode eixo x frequentemente é usada com a dimensão Tempo.  
  
 Depois de obter o conjunto de pontos, a função **LinRegR2** retorna o R<sup>2</sup> estatístico que descreve o ajuste da equação linear aos pontos.  
  
> [!NOTE]  
>  A função **LinRegR2** ignora células vazias ou células que contêm texto ou valores lógicos. Porém, a função contém células com valores zero.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o R<sup>2</sup> estatístico que descreve a importabilidade da equação de regressão linear para os pontos das vendas da unidade e das medidas de vendas da loja.  
  
```  
LinRegR2(LastPeriods(10), [Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
