---
title: Elemento (ASSL) do cubo | Microsoft Docs
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
- Cube Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Cube
helpviewer_keywords:
- Cube element
ms.assetid: 2d801066-6cca-4a99-bbd8-56a38d762108
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eab8cc56de346540491664a60c644ef868b02a25
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37165257"
---
# <a name="cube-element-assl"></a>Elemento Cube (ASSL)
  Define um cubo normal, virtual ou vinculado em uma [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] [banco de dados](database-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Cubes>  
   <Cube>  
            <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
            <Description>...</Description>  
            <Language>...</Language>  
            <Collation>...</Collation>  
            <Translations>...</Translations>  
      <Dimensions>...</Dimensions>  
            <CubePermissions>...</CubePermissions>  
      <MdxScripts>...</MdxScripts>  
      <Perspectives>...</Perspectives>  
      <State>...</State>  
      <DefaultMeasure>...</DefaultMeasure>  
      <Visible>...</Visible>  
      <MeasureGroups>...</MeasureGroups>  
      <DataSourceView >...</Source>  
      <AggregationPrefix>...</AggregationPrefix>  
      <ProcessingPriority>...</ProcessingPriority>  
            <StorageMode>...</StorageMode>  
      <ProcessingMode>...</ProcessingMode>  
      <ScriptCacheProcessingMode>...</ScriptCacheProcessingMode>  
      <ProactiveCaching>...</ProactiveCaching>  
            <Kpis>...</Kpis>  
            <ErrorConfiguration>...</ErrorConfiguration>  
            <Actions>...</Actions>  
      <StorageLocation>...</StorageLocation>  
      <EstimatedRows>...</EstimatedRows>  
      <LastProcessed>...</LastProcessed>  
      <Annotations>...</Annotations>  
   </Cube>  
</Cubes>  
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
|Elementos pai|[Cubos](../collections/cubes-element-assl.md)|  
|Elementos filho|[Ações](../collections/actions-element-assl.md), [AggregationPrefix](../properties/aggregationprefix-element-assl.md), [anotações](../collections/annotations-element-assl.md), [agrupamento](../properties/collation-element-assl.md), [CreatedTimestamp](../properties/createdtimestamp-element-assl.md), [ CubePermissions](../collections/cubepermissions-element-assl.md), [DefaultMeasure](measure-element-assl.md), [descrição](../properties/description-element-assl.md), [dimensões](../collections/dimensions-element-assl.md), [ErrorConfiguration](errorconfiguration-element-assl.md) , [EstimatedRows](../properties/estimatedrows-element-assl.md), [ID](../properties/id-element-assl.md), [Kpis](../collections/kpis-element-assl.md), [idioma](../properties/language-element-assl.md), [LastProcessed](../properties/lastprocessed-element-assl.md), [ LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [MdxScripts](../collections/mdxscripts-element-assl.md), [MeasureGroups](../collections/groups-element-assl.md), [nome](../properties/name-element-assl.md), [perspectivas](../collections/perspectives-element-assl.md), [ProactiveCaching](proactivecaching-element-assl.md), [ProcessingMode](../properties/processingmode-element-assl.md), [ProcessingPriority](../properties/processingpriority-element-assl.md), [ScriptCacheProcessingMode](../properties/scriptcacheprocessingmode-element-assl.md), [estado ](../properties/state-element-assl.md), [StorageLocation](../properties/storagelocation-element-assl.md), [StorageMode](../properties/storagemode-element-assl.md), [traduções](../collections/translations-element-assl.md), [visíveis](../properties/visible-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Cube>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
