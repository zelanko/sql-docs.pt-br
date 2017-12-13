---
title: Elemento ProactiveCaching (ASSL) | Microsoft Docs
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
apiname: ProactiveCaching Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ProactiveCaching
helpviewer_keywords: ProactiveCaching element
ms.assetid: 85f9ed44-2ede-406f-b0ca-237ab2f49722
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0ba62834dc35b82441f67d2175b6da26441f0cd8
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="proactivecaching-element-assl"></a>Elemento ProactiveCaching (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Define as configurações de cache pró-ativo para o elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Cube> <!-- or Dimension, MeasureGroup, Partition -->  
   ...  
   <ProactiveCaching>  
      <OnlineMode>...</OnlineMode>  
      <AggregationStorage>...</AggregationStorage>  
      <Source>...</Source>  
      <SilenceInterval>...</SilenceInterval>  
      <Latency>...</Latency>  
      <SilenceOverrideInterval>...</SilenceOverrideInterval>  
      <ForceRebuildInterval>...</ForceRebuildInterval>  
      <Enabled >...</Enabled>  
   </ProactiveCaching>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Cubo](../../../analysis-services/scripting/objects/cube-element-assl.md), [dimensão](../../../analysis-services/scripting/objects/dimension-element-assl.md), [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [partição](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|Elementos filho|[AggregationStorage](../../../analysis-services/scripting/properties/aggregationstorage-element-assl.md), [habilitado](../../../analysis-services/scripting/properties/enabled-element-assl.md), [ForceRebuildInterval](../../../analysis-services/scripting/properties/forcerebuildinterval-element-assl.md), [latência](../../../analysis-services/scripting/properties/latency-element-assl.md), [OnlineMode](../../../analysis-services/scripting/properties/onlinemode-element-assl.md), [ SilenceInterval](../../../analysis-services/scripting/properties/silenceinterval-element-assl.md), [SilenceOverrideInterval](../../../analysis-services/scripting/properties/silenceoverrideinterval-element-assl.md), [fonte](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.ProactiveCaching>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
