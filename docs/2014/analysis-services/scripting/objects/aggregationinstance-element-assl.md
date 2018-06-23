---
title: Elemento AggregationInstance (ASSL) | Microsoft Docs
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
api_name:
- AggregationInstance Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- AggregationInstance element
ms.assetid: 2e77e9e1-9f2c-4df4-9aa6-5b7b911016a3
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: fe8d4f62355888b9d145979af75ea312e32d554c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121364"
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[AggregationInstances](../collections/aggregationinstances-element-assl.md)|  
|Elementos filho|[AggregationID](../properties/id-element-assl.md), [AggregationType](../properties/aggregationtype-element-assl.md), [Annotations](../collections/annotations-element-assl.md), [Dimensions](../collections/dimensions-element-assl.md), [Measures](../collections/measures-element-assl.md), [Source](../properties/source-element-binding-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Quando um [partição](partition-element-assl.md) elemento usa um [AggregationDesign](aggregationdesign-element-assl.md) elemento para gerar agregações para essa partição, cada [agregação](aggregation-element-assl.md) no `AggregationDesign` é instanciada para essa partição. Várias partições podem usar o mesmo design de agregação para gerar várias instâncias de uma agregação definida. O elemento `AggregationInstance` representa uma instância de uma agregação definida.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.AggregationInstance>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  