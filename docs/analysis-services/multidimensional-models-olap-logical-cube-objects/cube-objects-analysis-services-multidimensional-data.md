---
title: Objetos (Analysis Services - dados multidimensionais) de cubo | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- cubes [Analysis Services], objects
ms.assetid: 5cee362e-3f95-4467-bc6c-29b1518ecbf3
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 018739c4f8da237c1a90a101b96888a8583349be
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="cube-objects-analysis-services---multidimensional-data"></a>Objetos cubo (Analysis Services – Dados Multidimensionais)
    
## <a name="introducing-cube-objects"></a>Apresentando objetos cubo  
 Um simples objeto <xref:Microsoft.AnalysisServices.Cube> é composto de: informações básicas, dimensões e grupos de medidas. As informações básicas incluem o nome do cubo, a medida padrão do cubo, a fonte de dados, o modo de armazenamento e outros.  
  
 A coleção Dimensões contém o conjunto real de dimensões usado no cubo da coleção de dimensões de banco de dados. Todas as dimensões precisam ser definidas na coleção de dimensões do banco de dados antes de serem referenciadas no cubo. Dimensões privadas não estão disponíveis em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Os grupos de medidas são conjuntos de medidas no cubo. Um grupo de medidas é uma coleção de medidas que têm uma fonte de dados e um conjunto de dimensões em comum. Um grupo de medidas é a unidade de processo para medidas; grupos de medidas podem ser processados individualmente e, em seguida, pesquisados.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|||  
|-|-|  
|Tópico||  
|[Ações &#40;Analysis Services – Dados Multidimensionais&#41;](../../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md)||  
|[Agregações e designs de agregação](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)||  
|[Cálculos](../../analysis-services/multidimensional-models-olap-logical-cube-objects/calculations.md)||  
|[Células de cubo &#40; Analysis Services - dados multidimensionais &#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-cells-analysis-services-multidimensional-data.md)||  
|[Programação de modelo de propriedades de cubo - Multidimensional](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-properties-multidimensional-model-programming.md)||  
|[Armazenamento de cubo &#40; Analysis Services - dados multidimensionais &#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-storage-analysis-services-multidimensional-data.md)||  
|[Traduções de cubo](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-translations.md)||  
|[Relações de dimensão](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)||  
|[Indicadores Chave de Desempenho &#40;KPIs&#41; em Modelos Multidimensionais](../../analysis-services/multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)||  
|[Medidas e grupos de medidas](../../analysis-services/multidimensional-models/measures-and-measure-groups.md)||  
|[Partições &#40;Analysis Services – Dados Multidimensionais&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)||  
|[Perspectivas](../../analysis-services/multidimensional-models-olap-logical-cube-objects/perspectives.md)||  
  
  

