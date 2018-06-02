---
title: Função Correlation (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e4b53ff01dc6cf0d62b334e95ac8a474f969f5f9
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34577448"
---
# <a name="correlation-mdx"></a>Função Correlation (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o coeficiente de correlação de pares x-y de valores avaliados em um conjunto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Correlation( Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Numeric_Expression_y*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número que representa valores do eixo y.  
  
 *Numeric_Expression_x*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número que representa valores do eixo x.  
  
## <a name="remarks"></a>Remarks  
 O **correlação** função calcula o coeficiente de correlação de dois pares de valores avaliando primeiro o conjunto especificado em relação a primeira expressão numérica para obter os valores para o eixo y. Em seguida, a função avalia o conjunto especificado em relação à segunda expressão numérica, se estiver presente, para obter o conjunto de valores para o eixo x. Se a segunda expressão numérica não for especificada, a função utilizará o contexto atual das células no conjunto especificado como os valores para o eixo x.  
  
> [!NOTE]  
>  O **correlação** função ignora células vazias ou células que contêm texto ou valores lógicos. Porém, a função contém células com valores zero.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
