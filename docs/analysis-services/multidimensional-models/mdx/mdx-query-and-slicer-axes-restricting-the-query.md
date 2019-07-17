---
title: Restringindo a consulta com a consulta e eixo do Slicer (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4ad9f1b3a60707a0a10c9b15865286e1ad53eb2c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208748"
---
# <a name="mdx-query-and-slicer-axes---restricting-the-query"></a>Consulta MDX e Eixos de segmentação – Restringir a consulta
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Ao formular uma instrução SELECT de expressões multidimensionais (MDX), normalmente um aplicativo analisa um cubo e divide o conjunto de hierarquias em dois subconjuntos:  
  
-   **Eixos de consulta**-o conjunto de hierarquias do qual os dados são recuperados para vários membros. Para obter mais informações sobre os eixos de consulta, consulte [Specifying the Contents of a Query Axis &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md) (Especificação do conteúdo de um eixo de consulta &#40;MDX&#41;).  
  
-   **Eixo do slicer**-o conjunto de hierarquias do qual os dados são recuperados para um único membro. Para obter mais informações sobre os eixos de slicer, consulte [Specifying the Contents of a Slicer Axis](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md) (Especificação do conteúdo de um eixo de consulta &#40;MDX&#41;).  
  
 Como os eixos de consulta e slicer podem ser construídos a partir de várias hierarquias do cubo que será consultado, esses termos são utilizados para diferenciar as hierarquias usadas pelo cubo que será consultado a partir das hierarquias criadas no cubo retornadas por uma consulta MDX.  
  
 Para ver um exemplo simples usando eixos de consulta e slicer, consulte [Using Query and Slicer Axes in a Simple Example &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-using-axes-in-a-simple-example.md) (Usando os eixos de consulta e de slicer em um exemplo simples &#40;MDX&#41;).  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com membros, tuplas e conjuntos &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)   
 [Conceitos básicos de consulta MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
