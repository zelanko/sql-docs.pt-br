---
title: Elemento MeasureGroup (ASSL) | Microsoft Docs
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
- MeasureGroup Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MeasureGroup
helpviewer_keywords:
- MeasureGroup element
ms.assetid: 7aa099db-5dc7-4cac-b437-f73fc0921b24
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 4f66d555ed09410985622fd2f5edb5d021b9d26c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007359"
---
# <a name="measuregroup-element-assl"></a>Elemento MeasureGroup (ASSL)
  Define um conjunto de medidas no mesmo nível de granularidade.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MeasureGroups>  
   <MeasureGroup> <!-- ancestor: Cube -->  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</<Create  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <Description>...</Description>  
      <LastProcessed>...</LastProcessed>  
      <Translations>...</Translations>  
      <Type>...</Type>  
      <State>...</State>  
      <MeasureQualification>...</MeasureQualification>  
      <Measures>...</Measures>  
      <DataAggregation>...</DataAggregation>  
      <Source>...</Source>  
            <StorageMode>...</StorageMode>  
      <StorageLocation>...</StorageLocation>  
      <IgnoreUnrelatedDimensions>...</IgnoreUnrelatedDimensions>  
            <ProactiveCaching>...</ProactiveCaching>  
      <EstimatedRows>...</EstimatedRows>  
      <ErrorConfiguration>...</ErrorConfiguration>  
      <EstimatedSize>...</EstimatedSize>  
      <ProcessingMode>...</ProcessingMode>  
      <Dimensions>...</Dimensions>  
      <Partitions>...</Partitions>  
      <AggregationPrefix>...</AggregationPrefix>  
      <ProcessingPriority>...</ProcessingPriority>  
            <AggregationDesigns>...</AggregationDesigns>  
      <Annotations>...</Annotations>  
   </MeasureGroup>  
   <!-- or  -->  
   <MeasureGroup xsi:type="MeasureGroupBinding">...</MeasureGroup> <!-- ancestor: CubeBinding -->  
   <!-- or  -->  
   <MeasureGroup xsi:type="PerspectiveMeasureGroup">...</MeasureGroup> <!-- ancestor: Perspective -->  
</MeasureGroups>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
|Ancestral ou pai|Tipo de Dados|  
|------------------------|---------------|  
|[Cube](cube-element-assl.md)|Nenhum|  
|[CubeBinding](../data-type/binding-data-type-assl.md)|  
|[Perspectiva](../data-type/perspectivemeasuregroup-data-type-assl.md)|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[MeasureGroups](../collections/groups-element-assl.md)|  
|Elementos filho||  
  
|Ancestral ou pai|Elementos filho|  
|------------------------|--------------------|  
|[Cube](../collections/aggregationdesigns-element-assl.md), [AggregationPrefix](../properties/aggregationprefix-element-assl.md), [Annotations](../collections/annotations-element-assl.md), [CreatedTimestamp](../properties/createdtimestamp-element-assl.md), [DataAggregation](aggregation-element-assl.md), [Description](../properties/description-element-assl.md), [Dimensions](../collections/dimensions-element-assl.md), [ErrorConfiguration](errorconfiguration-element-assl.md), [EstimatedRows](../properties/estimatedrows-element-assl.md), [EstimatedSize](../properties/estimatedsize-element-assl.md), [ID](../properties/id-element-assl.md), [IgnoreUnrelatedDimensions](../properties/ignoreunrelateddimensions-element-assl.md), [LastProcessed](../properties/lastprocessed-element-assl.md), [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [MeasureQualification](../properties/measurequalificaton-element-assl.md), [Measures](../collections/measures-element-assl.md), [Name](../properties/name-element-assl.md), [Partitions](../collections/partitions-element-assl.md), [ProactiveCaching](proactivecaching-element-assl.md), [ProcessingMode](../properties/processingmode-element-assl.md), [ProcessingPriority](../properties/processingpriority-element-assl.md), [Source](../properties/source-element-measure-assl.md), [State](../properties/state-element-assl.md), [StorageLocation](../properties/storagelocation-element-assl.md), [StorageMode](../properties/storagemode-element-assl.md), [Translations](../collections/translations-element-assl.md), [Type](../properties/type-element-measuregroup-assl.md)|  
|[CubeBinding](../data-type/cubebinding-data-type-out-of-line-assl.md)|Nenhum|  
|[Perspectiva](perspective-element-assl.md)|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Todas as medidas de um grupo de medidas devem se originar de uma única tabela. Um grupo de medidas pode definir associações padrão que podem ser substituídas para cada partição.  
  
 O elemento `MeasureGroup` define detalhes comuns a grupos de medidas em cubos normais e em cubos virtuais. Subtipos separados definem os detalhes específicos para cada tipo.  
  
 A propriedade `State` de um `MeasureGroup` tem os valores seguintes:  
  
-   *FullyProcessed* se todas as partições forem processadas.  
  
-   *PartiallyProcessed* se pelo menos uma partição for processada.  
  
-   *Unprocessed* se nenhuma partição for processada.  
  
 Os elementos correspondentes no modelo de objeto AMO (Objetos de Gerenciamento de Análise) são <xref:Microsoft.AnalysisServices.MeasureGroup> e <xref:Microsoft.AnalysisServices.PerspectiveMeasureGroup>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  