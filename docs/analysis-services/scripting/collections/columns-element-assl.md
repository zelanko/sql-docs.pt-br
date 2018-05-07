---
title: Elemento Columns (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ebff40f4dce500da857990ccba3f90351385e98f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="columns-element-assl"></a>Elemento Columns (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contém a coleção de colunas associada ao elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Action xsi:type="DrillThroughAction"> <!-- or one of the elements listed below in the Element Relationships table -->  
   <Columns>  
      <Column xsi:type="MeasureBinding">...</Column> <!-- parent: DrillThroughAction -->  
      <!-- or -->  
      <Column xsi:type="CubeAttributeBinding">...</Column> <!-- parent: DrillThroughAction -->  
      <!-- or -->  
      <Column xsi:type="EventColumn">...</Column> <!-- parent: Event -->  
      <!-- or -->  
      <Column xsi:type="MiningModelColumn">...</Column> <!-- parent: MiningModel or MiningModelColumn -->  
      <!-- or -->  
      <Column xsi:type="MiningStructureColumn">...</Column> <!-- parent: MiningStructure or TableMiningStructureColumn -->  
   </Columns>  
</DrillThroughAction>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|Veja a tabela abaixo.|  
  
|Ancestral ou pai|Cardinalidade|  
|------------------------|-----------------|  
|[Evento](../../../analysis-services/scripting/objects/event-element-assl.md)|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
|Todos os outros|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Ação](../../../analysis-services/scripting/objects/action-element-assl.md) do tipo [DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md), [evento](../../../analysis-services/scripting/objects/event-element-assl.md), [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md), [MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md), [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md), [TableMiningStructureColumn](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md)|  
|Elementos filho|Veja a tabela abaixo.|  
  
|Ancestral ou pai|Elementos filho|  
|------------------------|--------------------|  
|[DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)|[CubeAttributeBinding](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md) ou [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|  
|[Evento](../../../analysis-services/scripting/objects/event-element-assl.md)|[EventColumn](../../../analysis-services/scripting/data-type/eventcolumn-data-type-assl.md)|  
|[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md), [MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md)|[MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md)|  
|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md), [TableMiningStructureColumn](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md)|[MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Para elementos **DrillThroughAction** , a coleção **Columns** identifica as colunas que contêm dados a serem retornados quando a ação for executada.  
  
 Para elementos **TableMiningStructureColumn** , a coleção **Columns** permite só um nível de recursão. Em outras palavras, qualquer elemento **TableMiningStructureColumn** incluído nesta coleção não pode conter nenhum elemento **TableMiningStructureColumn** em sua coleção **Columns** .  
  
 Alguns dos elementos correspondentes no modelo de objeto AMO (Objetos de Gerenciamento de Análise) são <xref:Microsoft.AnalysisServices.TraceColumnCollection>, <xref:Microsoft.AnalysisServices.MiningModelColumnCollection> e <xref:Microsoft.AnalysisServices.MiningStructureColumnCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Coleções de & #40; ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
