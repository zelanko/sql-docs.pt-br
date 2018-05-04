---
title: Tipo de dados AggregationDesignDimension (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- AggregationDesignDimension Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AggregationDesignDimension
helpviewer_keywords:
- AggregationDesignDimension data type
ms.assetid: 06a0d418-014c-4f40-a63a-5cfeee3f6a41
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 9967906561190fdccba9c780d019c70c8cc29782
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="aggregationdesigndimension-data-type-assl"></a>Tipo de dados AggregationDesignDimension (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define um tipo de dados primitivo que representa a relação entre uma dimensão de cubo e um elemento [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AggregationDesignDimension>  
   <CubeDimensionID>...</CubeDimensionID>  
   <Attributes>...</Attributes>  
      <Annotations>...</Annotations>  
</AggregationDesignDimension>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|Nenhuma|  
|Tipos de dados derivados|Nenhuma|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|[Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md), [Attributes](../../../analysis-services/scripting/collections/attributes-element-assl.md), [CubeDimensionID](../../../analysis-services/scripting/properties/cubedimensionid-element-assl.md)|  
|Elementos derivados|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md) (coleção[Dimensions](../../../analysis-services/scripting/collections/dimensions-element-assl.md) de [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.AggregationDesignDimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento AggregationDesign & #40; ASSL & #41;](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)   
 [Tipos de dados XML de linguagem de script & #40; do Analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
