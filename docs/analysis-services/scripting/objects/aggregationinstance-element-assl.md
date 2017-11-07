---
title: Elemento AggregationInstance (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- AggregationInstance Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- AggregationInstance element
ms.assetid: 2e77e9e1-9f2c-4df4-9aa6-5b7b911016a3
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f9a3840c481d63b06357fa8c76b9f3fc7c2ae6bc
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="aggregationinstance-element-assl"></a>Elemento AggregationInstance (ASSL)
  Define uma instância de agregação para uma partição.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AggregationInstances>  
   <AggregationInstance>  
      <AggregationType>...</AggregationType>  
      <AggregationID>...</AggregationID>  
      <Source>...</Source>  
      <Dimensions>...</Dimensions>  
      <Measures>...</Measures>  
      <Annotations>...</Annotations>  
   </AggregationInstance>  
</AggregationInstances>  
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
|Elementos pai|[AggregationInstances](../../../analysis-services/scripting/collections/aggregationinstances-element-assl.md)|  
|Elementos filho|[AggregationID](../../../analysis-services/scripting/properties/aggregationid-element-assl.md), [AggregationType](../../../analysis-services/scripting/properties/aggregationtype-element-assl.md), [Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md), [Dimensions](../../../analysis-services/scripting/collections/dimensions-element-assl.md), [Measures](../../../analysis-services/scripting/collections/measures-element-assl.md), [Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 Quando um elemento [Partition](../../../analysis-services/scripting/objects/partition-element-assl.md) usa um elemento [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md) para gerar agregações para essa partição, cada [Aggregation](../../../analysis-services/scripting/objects/aggregation-element-assl.md) em **AggregationDesign** é instanciada para essa partição. Várias partições podem usar o mesmo design de agregação para gerar várias instâncias de uma agregação definida. O elemento **AggregationInstance** representa uma instância de uma agregação definida.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.AggregationInstance>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

