---
title: Objetos (Analysis Services - dados multidimensionais) de cubo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- cubes [Analysis Services], objects
ms.assetid: 5cee362e-3f95-4467-bc6c-29b1518ecbf3
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 783caa7a2ea334da09ab038694c09795fa3af229
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36011493"
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
|[Ações &#40;Analysis Services - dados multidimensionais&#41;](../multidimensional-models/actions-analysis-services-multidimensional-data.md)||  
|[Agregações e designs de agregação](aggregations-and-aggregation-designs.md)||  
|[Cálculos](calculations.md)||  
|[Células de cubo &#40;Analysis Services - dados multidimensionais&#41;](cube-cells-analysis-services-multidimensional-data.md)||  
|[Propriedades do cubo](cube-properties-multidimensional-model-programming.md)||  
|[Armazenamento de cubo &#40;Analysis Services - dados multidimensionais&#41;](cube-storage-analysis-services-multidimensional-data.md)||  
|[Conversões de cubo](cube-translations.md)||  
|[Relações de dimensão](dimension-relationships.md)||  
|[Indicadores chave de desempenho &#40;KPIs&#41; em modelos multidimensionais](../multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)||  
|[Medidas e grupos de medidas](../multidimensional-models/measures-and-measure-groups.md)||  
|[Partições &#40;Analysis Services - dados multidimensionais&#41;](partitions-analysis-services-multidimensional-data.md)||  
|[Perspectivas](perspectives.md)||  
  
  