---
title: Restringindo a consulta com a consulta e o eixo do Slicer (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], axes
- queries [MDX], axes
- axes [MDX]
- MDX [Analysis Services], axes
ms.assetid: a64b8172-cd73-42f9-8847-52e967b9697a
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 2ae437951601f639cc114fcde470d97fa1685eb7
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="mdx-query-and-slicer-axes---restricting-the-query"></a>Eixo da segmentação de dados - restringindo a consulta e consulta MDX
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Ao formular uma instrução SELECT MDX (Multidimensional Expressions), um aplicativo normalmente analisa um cubo e divide o conjunto de hierarquias em dois subconjuntos:  
  
-   **Eixos de consulta**– o conjunto de hierarquias por meio do qual são recuperados dados para vários membros. Para obter mais informações sobre os eixos de consulta, consulte [Specifying the Contents of a Query Axis &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md) (Especificação do conteúdo de um eixo de consulta &#40;MDX&#41;).  
  
-   **Eixo de slicer**— o conjunto de hierarquias do qual são recuperados dados para um único membro. Para obter mais informações sobre os eixos de slicer, consulte [Specifying the Contents of a Slicer Axis](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md) (Especificação do conteúdo de um eixo de consulta &#40;MDX&#41;).  
  
 Como os eixos de consulta e slicer podem ser construídos a partir de várias hierarquias do cubo que será consultado, esses termos são utilizados para diferenciar as hierarquias usadas pelo cubo que será consultado a partir das hierarquias criadas no cubo retornadas por uma consulta MDX.  
  
 Para ver um exemplo simples usando eixos de consulta e slicer, consulte [Using Query and Slicer Axes in a Simple Example &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-using-axes-in-a-simple-example.md) (Usando os eixos de consulta e de slicer em um exemplo simples &#40;MDX&#41;).  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com membros, tuplas e conjuntos &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)   
 [Conceitos básicos de consulta MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
