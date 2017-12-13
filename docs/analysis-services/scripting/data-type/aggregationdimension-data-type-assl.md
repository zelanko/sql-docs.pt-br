---
title: Tipo de dados AggregationDimension (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
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
apiname: AggregationDimension Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AggregationDimension
helpviewer_keywords: AggregationDimension data type
ms.assetid: 697e0e09-3210-4a56-882f-80726abc4c68
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: cd73d9a355f19357ea22f5554d56dfe4eaaff6d6
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="aggregationdimension-data-type-assl"></a>Tipo de dados AggregationDimension (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Define um tipo de dados primitivo que representa a relação entre uma dimensão e um [agregação](../../../analysis-services/scripting/objects/aggregation-element-assl.md) elemento.  
  
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
|Elementos filho|[Anotações](../../../analysis-services/scripting/collections/annotations-element-assl.md), [atributos](../../../analysis-services/scripting/collections/attributes-element-assl.md), [CubeDimensionID](../../../analysis-services/scripting/properties/cubedimensionid-element-assl.md)|  
|Elementos derivados|[Dimensão](../../../analysis-services/scripting/objects/dimension-element-assl.md) ([dimensões](../../../analysis-services/scripting/collections/dimensions-element-assl.md) coleção de [agregação](../../../analysis-services/scripting/objects/aggregation-element-assl.md))|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.AggregationDimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script &#40; do Analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
