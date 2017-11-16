---
title: "Conceitos básicos de consulta MDX (Analysis Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- statements [MDX]
- Multidimensional Expressions [Analysis Services], statements
- Multidimensional Expressions [Analysis Services], queries
- MDX [Analysis Services], statements
- MDX queries [Analysis Services]
- MDX [Analysis Services], queries
- queries [MDX]
ms.assetid: a560383b-bb58-472e-95f5-65d03d8ea08b
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cefad04fdadd4475863dccca5cba5f3e9cf4f48c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-query-fundamentals-analysis-services"></a>Conceitos básicos de consulta MDX (Analysis Services)
  O MDX (Multidimensional Expressions) permite que você consulte objetos multidimensionais, como cubos, e retorna conjuntos de células multidimensionais que contêm dados do cubo. Este tópico e respectivos subtópicos fornecem uma visão geral das consultas MDX.  
  
 Os tópicos a seguir descrevem consultas MDX e os conjuntos de células que elas produzem, e fornecem informações mais detalhadas sobre a sintaxe básica de MDX.  
  
> [!NOTE]  
>  Para obter mais informações sobre questões de desempenho relacionadas a cálculos e consultas MDX, consulte a seção “Writing Efficient MDX” (Escrevendo um MDX eficiente) no [SQL Server 2005 Analysis Services Performance Guide](http://go.microsoft.com/fwlink/?LinkId=81621)(Guia de desempenho do SQL Server 2005 Analysis Services).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[A consulta básica de MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query.md)|Fornece informações de sintaxe básica para a instrução MDX SELECT.|  
|[Restringindo a consulta com a consulta e o eixo da segmentação de dados &#40; MDX &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-restricting-the-query.md)|Descreve o que são eixos de consulta e slicer e como os especificá-los.|  
|[Estabelecendo o contexto de cubo em uma consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md)|Fornece uma descrição sobre a finalidade da cláusula FROM em uma instrução MDX SELECT.|  
|[Criando conjuntos nomeados em MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets.md)|Descreve a finalidade de conjuntos nomeados em MDX e as técnicas necessárias para criá-los e usá-los em consultas MDX.|  
|[Criando membros calculados em MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-building-calculated-members.md)|Fornece informações sobre membros calculados em MDX, incluindo as técnicas necessárias para criá-los e usá-los em expressões MDX.|  
|[Criando cálculos de célula em MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-build-cell-calculations.md)|Detalha o processo de criação e utilização de células calculadas.|  
|[Criando e usando valores de propriedade &#40;MDX&#41;](http://msdn.microsoft.com/library/0cafb269-03c8-4183-b6e9-220f071e4ef2)|Detalha o processo de criação e utilização de dimensão, nível, membro e propriedades de célula.|  
|[Manipulando dados &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-manipulating-data.md)|Descreve os fundamentos inerentes da manipulação de dados usando o detalhamento e a representação acumulada, e também descreve a ordem de passagem e a ordem de resolução no MDX.|  
|[Modificando dados &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-modification-modifying-data.md)|Descreve como usar write-backs para alterar temporária ou permanentemente os dados multidimensionais.|  
|[Usando variáveis e parâmetros &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/using-variables-and-parameters-mdx.md)|Descreve como utilizar variáveis e parâmetros em consultas MDX.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de expressões multidimensionais &#40;MDX&#41;](../../../mdx/multidimensional-expressions-mdx-reference.md)  
  
  

