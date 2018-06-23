---
title: Elemento Columns (ASSL) | Microsoft Docs
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
- Columns Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- COLUMNS
helpviewer_keywords:
- Columns element
ms.assetid: 14011eed-6f10-4120-b256-d599d59bde80
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e635738dddc7eabda62f0c35df860db3d9a10b60
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013200"
---
# <a name="columns-element-assl"></a>Elemento Columns (ASSL)
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
  
|Ancestral ou pai|Cardinalidade|  
|------------------------|-----------------|  
|[Evento](../objects/event-element-assl.md)|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
|Todos os outros|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Ação](../objects/action-element-assl.md) do tipo [DrillThroughAction](../data-type/action-data-type-assl.md), [evento](../objects/event-element-assl.md), [MiningModel](../objects/miningmodel-element-assl.md), [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md), [ MiningStructure](../objects/miningstructure-element-assl.md), [TableMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
  
|Ancestral ou pai|Elementos filho|  
|------------------------|--------------------|  
|[DrillThroughAction](../data-type/binding-data-type-assl.md) ou [MeasureBinding](../data-type/measurebinding-data-type-assl.md)|  
|[Evento](../data-type/eventcolumn-data-type-assl.md)|  
|[MiningModel](../objects/miningmodel-element-assl.md), [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)|[MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)|  
|[MiningStructure](../objects/miningstructure-element-assl.md), [TableMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|[MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Para `DrillThroughAction` elementos, o `Columns` coleção identifica as colunas que contêm os dados a serem retornados quando a ação é executada.  
  
 Para `TableMiningStructureColumn` elementos, o `Columns` coleção permite apenas um nível de recursão. Em outras palavras, qualquer `TableMiningStructureColumn` elemento incluído nesta coleção não pode conter nenhum `TableMiningStructureColumn` elementos no seu `Columns` coleção.  
  
 Alguns dos elementos correspondentes no modelo de objeto AMO (Objetos de Gerenciamento de Análise) são <xref:Microsoft.AnalysisServices.TraceColumnCollection>, <xref:Microsoft.AnalysisServices.MiningModelColumnCollection> e <xref:Microsoft.AnalysisServices.MiningStructureColumnCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Coleções &#40;ASSL&#41;](collections-assl.md)  
  
  