---
title: "Elemento (ASSL) de dimensão | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
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
apiname: Dimension Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Dimension
helpviewer_keywords: Dimension element
ms.assetid: 71886014-f463-4b70-a2a2-d9e5053ba4f0
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1853870b364f958ed279c8d7de6e219fe7cab412
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="dimension-element-assl"></a>Elemento Dimension (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Define uma dimensão.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Dimensions>  
   <Dimension xsi:type="Dimension">...</Dimension> <!-- ancestor: Database -->  
   <!-- or -->  
   <Dimension xsi:type="AggregationDimension">...</Dimension> <!-- ancestor: Aggregation -->  
   <!-- or -->  
   <Dimension xsi:type="AggregationDesignDimension">...</Dimension> <!-- ancestor: AggregationDesign -->  
   <!-- or -->  
   <Dimension xsi:type="AggregationInstanceCubeDimension">...</Dimension> <!-- ancestor: AggregationInstance -->  
      <!-- or -->  
   <Dimension xsi:type="CubeDimension">...</Dimension> <!-- ancestor: Cube -->  
      <!-- or -->  
   <Dimension xsi:type="MeasureGroupDimension">...</Dimension> <!-- ancestor: MeasureGroup -->  
   <!-- or -->  
   <Dimension xsi:type="PerspectiveDimension">...</Dimension> <!-- ancestor: Perspective -->  
</Dimensions>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Consulte a tabela a seguir.|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
|Ancestral ou pai|Tipo de Dados|  
|------------------------|---------------|  
|[Banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md)|[Dimension](../../../analysis-services/scripting/data-type/dimension-data-type-assl.md)|  
|[Agregação](../../../analysis-services/scripting/objects/aggregation-element-assl.md)|[AggregationDimension](../../../analysis-services/scripting/data-type/aggregationdimension-data-type-assl.md)|  
|[AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)|[AggregationDesignDimension](../../../analysis-services/scripting/data-type/aggregationdesigndimension-data-type-assl.md)|  
|[AggregationInstance](../../../analysis-services/scripting/objects/aggregationinstance-element-assl.md)|[AggregationInstanceCubeDimension](../../../analysis-services/scripting/data-type/aggregationinstancecubedimension-data-type-assl.md)|  
|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)|[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)|  
|[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|[MeasureGroupDimension](../../../analysis-services/scripting/data-type/measuregroupdimension-data-type-assl.md)|  
|[Perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md)|[PerspectiveDimension](../../../analysis-services/scripting/data-type/perspectivedimension-data-type-assl.md)|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Dimensions](../../../analysis-services/scripting/collections/dimensions-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Os elementos correspondentes no modelo de objeto Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.AggregationDimension>, <xref:Microsoft.AnalysisServices.AggregationDesignDimension>, <xref:Microsoft.AnalysisServices.CubeDimension>, <xref:Microsoft.AnalysisServices.MeasureGroupDimension>, e <xref:Microsoft.AnalysisServices.PerspectiveDimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
