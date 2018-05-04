---
title: Tipo de dados AggregationDimension (ASSL) | Microsoft Docs
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
- AggregationDimension Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AggregationDimension
helpviewer_keywords:
- AggregationDimension data type
ms.assetid: 697e0e09-3210-4a56-882f-80726abc4c68
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2dd4230312ca4dbe4adf1ffe0ac98a6769a29507
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="aggregationdimension-data-type-assl"></a>Tipo de dados AggregationDimension (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define um tipo de dados primitivo que representa a relação entre uma dimensão e um elemento [Aggregation](../../../analysis-services/scripting/objects/aggregation-element-assl.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AggregationDimension>  
   <CubeDimensionID>...</CubeDimensionID>  
   <Attributes>...</Attributes>  
      <Annotations>...</Annotations>  
</AggregationDimension>  
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
|Elementos derivados|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md) (coleção[Dimensions](../../../analysis-services/scripting/collections/dimensions-element-assl.md) de [Aggregation](../../../analysis-services/scripting/objects/aggregation-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.AggregationDimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script & #40; do Analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
