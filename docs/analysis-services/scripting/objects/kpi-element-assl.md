---
title: Elemento KPI (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
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
- Kpi Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Kpi
helpviewer_keywords:
- Kpi element
ms.assetid: 1979a58f-97a8-4c1a-aa65-dcfb6d2404cf
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 902b4e834da88b9ed89ed09915cda952d20a6edb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="kpi-element-assl"></a>Elemento Kpi (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define um KPI (indicador chave de desempenho) em um elemento [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) ou em um elemento [Perspective](../../../analysis-services/scripting/objects/perspective-element-assl.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Kpis>  
   <Kpi> <!-- ancestor: Cube -->  
            <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</Description>  
      <Translations>...</Translations>  
      <DisplayFolder>...</DisplayFolder>  
      <AssociatedMeasureGroupID>...</AssociatedMeasureGroupID>  
      <Value>...</Value>  
            <Goal>...</Goal>  
      <Status>...</Status>  
      <Trend>...</Trend>  
      <TrendGraphic>...</TrendGraphic>  
      <StatusGraphic>...</StatusGraphic>  
      <CurrentTimeMember>...</CurrentTimeMember>  
      <Annotations>...</Annotations>  
   </Kpi>  
   <!-- or -->  
   <Kpi xsi:type="PerspectiveKpi">...</Kpi> <!-- ancestor: Perspective -->  
   </Kpi>  
</Kpis>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Veja a tabela abaixo.|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
|Ancestral ou pai|Tipo de Dados|  
|------------------------|---------------|  
|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)|Nenhuma|  
|[Perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md)|[PerspectiveKpi](../../../analysis-services/scripting/data-type/perspectivekpi-data-type-assl.md)|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[KPIs](../../../analysis-services/scripting/collections/kpis-element-assl.md)|  
|Elementos filho|Veja a tabela abaixo.|  
  
|Ancestral ou pai|Elementos filho|  
|------------------------|--------------------|  
|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)|[Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md), [AssociatedMeasureGroupID](../../../analysis-services/scripting/properties/associatedmeasuregroupid-element-assl.md), [CurrentTimeMember](../../../analysis-services/scripting/properties/currenttimemember-element-assl.md), [Description](../../../analysis-services/scripting/properties/description-element-assl.md), [DisplayFolder](../../../analysis-services/scripting/properties/displayfolder-element-assl.md), [Goal](../../../analysis-services/scripting/properties/goal-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [Name](../../../analysis-services/scripting/properties/name-element-assl.md), [Status](../../../analysis-services/scripting/properties/status-element-assl.md), [StatusGraphic](../../../analysis-services/scripting/properties/statusgraphic-element-assl.md), [Translations](../../../analysis-services/scripting/collections/translations-element-assl.md), [Trend](../../../analysis-services/scripting/properties/trend-element-assl.md), [TrendGraphic](../../../analysis-services/scripting/properties/trendgraphic-element-assl.md), [Value](../../../analysis-services/scripting/properties/value-element-assl.md)|  
|[Perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md)|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 Os elementos correspondentes no modelo de objeto AMO (Objetos de Gerenciamento de Análise) são <xref:Microsoft.AnalysisServices.Kpi> e <xref:Microsoft.AnalysisServices.PerspectiveKpi>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
