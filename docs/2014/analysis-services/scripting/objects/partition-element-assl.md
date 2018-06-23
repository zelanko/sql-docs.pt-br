---
title: Elemento (ASSL) da partição | Microsoft Docs
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
- Partition Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- PARTITION
helpviewer_keywords:
- Partition element
ms.assetid: 40020840-1bb7-478f-9017-1a30342ac4c6
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 371c6fbb2d77993a0d6113101c0f074b88009ede
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012779"
---
# <a name="partition-element-assl"></a>Elemento Partition (ASSL)
  Define uma partição de um [MeasureGroup](group-element-assl.md) elemento ou uma associação de partição em uma limite de linha [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-out-of-line-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Partitions>  
      <Partition> <!-- ancestor: MeasureGroup -->  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <Description>...</Description>  
      <Source>...</Source>  
      <ProcessingPriority>...</ProcessingPriority>  
      <AggregationPrefix>...</AggregationPrefix>  
      <StorageMode>...</StorageMode>  
      <ProcessingMode>...</ProcessingMode>  
      <ErrorConfiguration>...</ErrorConfiguration>  
      <StorageLocation>...</StorageLocation>  
      <RemoteDatasourceID>...</RemoteDatasourceID>  
      <Slice>...</Slice>  
      <ProactiveCaching>...</ProactiveCaching>  
      <Type>...</Type>  
      <EstimatedSize>...</EstimatedSize>  
      <EstimatedRows>...</EstimatedRows>  
      <CurrentStorageMode>...</CurrentStorageMode>  
      <AggregationDesignID>...</AggregationDesignID>  
      <AggregationInstances>...</AggregationInstances>  
      <AggregationInstanceSource>...</AggregationInstanceSource>  
      <LastProcessed>...</LastProcessed>  
      <State>...</State>  
      <Annotations>.../Annotations>  
   </Partition>  
   <!-- or -->  
   <Partition xsi:type="PartitionBinding"> <!-- ancestor: MeasureGroupBinding -->  
   </Partition>  
</Partitions>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
|Ancestral ou pai|Tipo de Dados|  
|------------------------|---------------|  
|[MeasureGroup](group-element-assl.md)|Nenhum|  
|[MeasureGroupBinding](../data-type/binding-data-type-assl.md)|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Partições](../collections/partitions-element-assl.md)|  
  
|Ancestral ou pai|Elementos filho|  
|------------------------|--------------------|  
|[MeasureGroup](../properties/id-element-assl.md), [AggregationInstances](../collections/aggregationinstances-element-assl.md), [AggregationInstanceSource](../properties/aggregationinstancesource-element-assl.md), [AggregationPrefix](../properties/aggregationprefix-element-assl.md), [Annotations](../collections/annotations-element-assl.md), [CreatedTimestamp](../properties/createdtimestamp-element-assl.md), [CurrentStorageMode](../properties/storagemode-element-assl.md), [Description](../properties/description-element-assl.md), [ErrorConfiguration](errorconfiguration-element-assl.md), [EstimatedRows](../properties/estimatedrows-element-assl.md), [EstimatedSize](../properties/estimatedsize-element-assl.md), [ID](../properties/id-element-assl.md), [LastProcessed](../properties/lastprocessed-element-assl.md), [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [Name](../properties/name-element-assl.md), [ProactiveCaching](proactivecaching-element-assl.md), [ProcessingMode](../properties/processingmode-element-assl.md), [ProcessingPriority](../properties/processingpriority-element-assl.md), [RemoteDatasourceID](../properties/datasourceid-element-assl.md), [Slice](../properties/slice-element-assl.md), [Source](../properties/source-element-binding-assl.md), [State](../properties/state-element-assl.md), [StorageLocation](../properties/storagelocation-element-assl.md), [StorageMode](../properties/storagemode-element-assl.md), [Type](../properties/type-element-partition-assl.md)|  
|[MeasureGroupBinding](../data-type/measuregroupbinding-data-type-out-of-line-assl.md)|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Este elemento tem as validações a seguir no valor 2 DeploymentMode (modo de servidor de tabela):  
  
-   Os elementos de filhos a seguir não têm suporte e não devem ser usados:  
  
    -   [ProcessingPriority](../properties/processingpriority-element-assl.md)  
  
    -   [AggregationPrefix](../properties/aggregationprefix-element-assl.md)  
  
    -   [StorageLocation](../properties/storagelocation-element-assl.md)  
  
    -   [ProcessingMode](../properties/processingmode-element-assl.md)  
  
    -   [ErrorConfiguration](errorconfiguration-element-assl.md)  
  
    -   [StorageLocation](../properties/storagelocation-element-assl.md)  
  
    -   [RemoteDatasourceID](../properties/datasourceid-element-assl.md)  
  
    -   [Fatia](../properties/slice-element-assl.md)  
  
    -   [ProactiveCaching](proactivecaching-element-assl.md)  
  
    -   [Tipo](../properties/type-element-partition-assl.md)  
  
    -   [CurrentStorageMode](../properties/storagemode-element-assl.md)  
  
    -   [AggregationDesignID](../properties/aggregationdesignid-element-assl.md)  
  
    -   [AggregationInstances](../collections/aggregationinstances-element-assl.md)  
  
    -   [AggregationInstanceSource](../properties/aggregationinstancesource-element-assl.md)  
  
     Um erro pode ser gerado se algum dos elementos acima for usado.  
  
-   O [fonte](../properties/source-element-binding-assl.md) elemento aceita apenas **consulta** associação.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Partition>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  