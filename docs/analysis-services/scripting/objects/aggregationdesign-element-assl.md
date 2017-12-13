---
title: Elemento AggregationDesign (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: AggregationDesign Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AggregationDesign
helpviewer_keywords: AggregationDesign element
ms.assetid: 80ad98d8-73a8-4353-b5ad-d2a9ac3bc531
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 48a9fb564e4938f70d0bcdfeba5949572d6069cd
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="aggregationdesign-element-assl"></a>Elemento AggregationDesign (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Define um conjunto de definições de agregação que pode ser compartilhado por várias partições em um banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AggregationDesigns>  
   <AggregationDesign>  
      <ID>...</ID>  
      <Name>...</Name>  
            <Description>...</Description>  
      <EstimatedRows>...</EstimatedRows>  
      <Dimensions>...</Dimensions>  
            <Aggregations>...</Aggregation>  
      <EstimatedPerformanceGain>...</EstimatedPerformanceGain>  
      <Annotations>...</Annotations>  
   </AggregationDesign>  
</AggregationDesigns>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[AggregationDesigns](../../../analysis-services/scripting/collections/aggregationdesigns-element-assl.md)|  
|Elementos filho|[Agregações](../../../analysis-services/scripting/collections/aggregations-element-assl.md), [anotações](../../../analysis-services/scripting/collections/annotations-element-assl.md), [descrição](../../../analysis-services/scripting/properties/description-element-assl.md), [dimensões](../../../analysis-services/scripting/collections/dimensions-element-assl.md), [EstimatedPerformanceGain](../../../analysis-services/scripting/properties/estimatedperformancegain-element-assl.md), [EstimatedRows](../../../analysis-services/scripting/properties/estimatedrows-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [nome](../../../analysis-services/scripting/properties/name-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.AggregationDesign>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Partition &#40; ASSL &#41;](../../../analysis-services/scripting/objects/partition-element-assl.md)   
 [Elemento Aggregation &#40; ASSL &#41;](../../../analysis-services/scripting/objects/aggregation-element-assl.md)   
 [Elemento Aggregations &#40; ASSL &#41;](../../../analysis-services/scripting/collections/aggregations-element-assl.md)   
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
