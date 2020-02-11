---
title: Restringindo a consulta com os eixos de consulta e de segmentação (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], axes
- queries [MDX], axes
- axes [MDX]
- MDX [Analysis Services], axes
ms.assetid: a64b8172-cd73-42f9-8847-52e967b9697a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3290bc5892280cda5e8042de79ff581b305e8ec3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66074037"
---
# <a name="restricting-the-query-with-query-and-slicer-axes-mdx"></a>Restringindo a consulta com os eixos de consulta e slicer (MDX)
  Ao formular uma instrução SELECT de expressões multidimensionais (MDX), normalmente um aplicativo analisa um cubo e divide o conjunto de hierarquias em dois subconjuntos:  
  
-   **Eixos de consulta**-o conjunto de hierarquias do qual os dados são recuperados para vários membros. Para obter mais informações sobre os eixos de consulta, consulte [Specifying the Contents of a Query Axis &#40;MDX&#41;](mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md) (Especificação do conteúdo de um eixo de consulta &#40;MDX&#41;).  
  
-   **Eixo da segmentação**-o conjunto de hierarquias do qual os dados são recuperados para um único membro. Para obter mais informações sobre os eixos de slicer, consulte [Specifying the Contents of a Slicer Axis](mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md) (Especificação do conteúdo de um eixo de consulta &#40;MDX&#41;).  
  
 Como os eixos de consulta e slicer podem ser construídos a partir de várias hierarquias do cubo que será consultado, esses termos são utilizados para diferenciar as hierarquias usadas pelo cubo que será consultado a partir das hierarquias criadas no cubo retornadas por uma consulta MDX.  
  
 Para ver um exemplo simples usando eixos de consulta e slicer, consulte [Using Query and Slicer Axes in a Simple Example &#40;MDX&#41;](mdx-query-and-slicer-axes-using-axes-in-a-simple-example.md) (Usando os eixos de consulta e de slicer em um exemplo simples &#40;MDX&#41;).  
  
## <a name="see-also"></a>Consulte Também  
 [Trabalhando com membros, tuplas e conjuntos &#40;&#41;MDX](working-with-members-tuples-and-sets-mdx.md)   
 [Conceitos básicos de consulta MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
