---
title: Objetos de cubo (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- cubes [Analysis Services], objects
ms.assetid: 5cee362e-3f95-4467-bc6c-29b1518ecbf3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fc9b813f5310acad9d6dfa2b844adae6168fc1f9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62702642"
---
# <a name="cube-objects-analysis-services---multidimensional-data"></a>Objetos cubo (Analysis Services – Dados Multidimensionais)
    
## <a name="introducing-cube-objects"></a>Apresentando objetos cubo  
 Um simples objeto <xref:Microsoft.AnalysisServices.Cube> é composto de: informações básicas, dimensões e grupos de medidas. As informações básicas incluem o nome do cubo, a medida padrão do cubo, a fonte de dados, o modo de armazenamento e outros.  
  
 A coleção Dimensões contém o conjunto real de dimensões usado no cubo da coleção de dimensões de banco de dados. Todas as dimensões precisam ser definidas na coleção de dimensões do banco de dados antes de serem referenciadas no cubo. As dimensões privadas não estão disponíveis [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]no.  
  
 Os grupos de medidas são conjuntos de medidas no cubo. Um grupo de medidas é uma coleção de medidas que têm uma fonte de dados e um conjunto de dimensões em comum. Um grupo de medidas é a unidade de processo para medidas; grupos de medidas podem ser processados individualmente e, em seguida, pesquisados.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|||  
|-|-|  
|Tópico||  
|[Ações &#40;Analysis Services – Dados Multidimensionais&#41;](../multidimensional-models/actions-analysis-services-multidimensional-data.md)||  
|[Agregações e designs de agregação](aggregations-and-aggregation-designs.md)||  
|[Cálculos](calculations.md)||  
|[As células de cubo &#40;Analysis Services de dados multidimensionais&#41;](cube-cells-analysis-services-multidimensional-data.md)||  
|[Propriedades do cubo](cube-properties-multidimensional-model-programming.md)||  
|[&#40;de armazenamento de cubos Analysis Services dados multidimensionais&#41;](cube-storage-analysis-services-multidimensional-data.md)||  
|[Traduções de cubo](cube-translations.md)||  
|[Relações de dimensão](dimension-relationships.md)||  
|[Indicadores Chave de Desempenho &#40;KPIs&#41; em Modelos Multidimensionais](../multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)||  
|[Medidas e Grupos de Medidas](../multidimensional-models/measures-and-measure-groups.md)||  
|[Partições &#40;Analysis Services – Dados Multidimensionais&#41;](partitions-analysis-services-multidimensional-data.md)||  
|[perspectivas](perspectives.md)||  
  
  
