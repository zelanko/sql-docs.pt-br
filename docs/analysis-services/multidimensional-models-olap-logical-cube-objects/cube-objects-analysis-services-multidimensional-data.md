---
title: Objetos (Analysis Services - dados multidimensionais) de cubo | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cada8410f608816272b159c66196fb761e510abe
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="cube-objects-analysis-services---multidimensional-data"></a>Objetos cubo (Analysis Services – Dados Multidimensionais)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
    
## <a name="introducing-cube-objects"></a>Apresentando objetos cubo  
 Um simples objeto <xref:Microsoft.AnalysisServices.Cube> é composto de: informações básicas, dimensões e grupos de medidas. As informações básicas incluem o nome do cubo, a medida padrão do cubo, a fonte de dados, o modo de armazenamento e outros.  
  
 A coleção Dimensões contém o conjunto real de dimensões usado no cubo da coleção de dimensões de banco de dados. Todas as dimensões precisam ser definidas na coleção de dimensões do banco de dados antes de serem referenciadas no cubo. Dimensões privadas não estão disponíveis em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Os grupos de medidas são conjuntos de medidas no cubo. Um grupo de medidas é uma coleção de medidas que têm uma fonte de dados e um conjunto de dimensões em comum. Um grupo de medidas é a unidade de processo para medidas; grupos de medidas podem ser processados individualmente e, em seguida, pesquisados.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|||  
|-|-|  
|Tópico||  
|[Ações & #40; Analysis Services - dados multidimensionais & #41;](../../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md)||  
|[Agregações e Designs de agregação](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)||  
|[Cálculos](../../analysis-services/multidimensional-models-olap-logical-cube-objects/calculations.md)||  
|[Células de cubo & #40; Analysis Services - dados multidimensionais & #41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-cells-analysis-services-multidimensional-data.md)||  
|[Propriedades do cubo – Programação de modelo multidimensional](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-properties-multidimensional-model-programming.md)||  
|[Armazenamento de cubo & #40; Analysis Services - dados multidimensionais & #41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-storage-analysis-services-multidimensional-data.md)||  
|[Traduções de cubo](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-translations.md)||  
|[Relações de dimensão](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)||  
|[Indicadores chave de desempenho & #40; KPIs & #41; em modelos multidimensionais](../../analysis-services/multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)||  
|[Medidas e grupos de medidas](../../analysis-services/multidimensional-models/measures-and-measure-groups.md)||  
|[Partições & #40; Analysis Services - dados multidimensionais & #41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)||  
|[Perspectivas](../../analysis-services/multidimensional-models-olap-logical-cube-objects/perspectives.md)||  
  
  
