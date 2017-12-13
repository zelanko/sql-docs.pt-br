---
title: Tipo de dados RegularMeasureGroupDimension (ASSL) | Microsoft Docs
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
apiname: RegularMeasureGroupDimension Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: RegularMeasureGroupDimension
helpviewer_keywords: RegularMeasureGroupDimension data type
ms.assetid: 5c4ce400-6d7c-40fc-9bcb-392718b77182
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5ea868b276a682a362d10608a58849e1f2cf99a7
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="regularmeasuregroupdimension-data-type-assl"></a>Tipo de dados RegularMeasureGroupDimension (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Define um tipo de dados derivado que representa uma relação regular entre uma dimensão e um grupo de medidas.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<RegularMeasureGroupDimension>  
   <!-- The following elements extend MeasureGroupDimension -->  
   <Cardinality>...</Cardinality>  
   <Attributes>...</Attributes>  
</RegularMeasureGroupDimension>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|[MeasureGroupDimension](../../../analysis-services/scripting/data-type/measuregroupdimension-data-type-assl.md)|  
|Tipos de dados derivados|[ReferenceMeasureGroupDimension](../../../analysis-services/scripting/data-type/referencemeasuregroupdimension-data-type-assl.md), [DegenerateMeasureGroupDimension](../../../analysis-services/scripting/data-type/degeneratemeasuregroupdimension-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|[Atributos](../../../analysis-services/scripting/collections/attributes-element-assl.md), [cardinalidade](../../../analysis-services/scripting/properties/cardinality-element-assl.md)|  
|Elementos derivados|[Dimensão](../../../analysis-services/scripting/objects/dimension-element-assl.md) ([dimensões](../../../analysis-services/scripting/collections/dimensions-element-assl.md) coleção)|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.RegularMeasureGroupDimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script &#40; do Analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
