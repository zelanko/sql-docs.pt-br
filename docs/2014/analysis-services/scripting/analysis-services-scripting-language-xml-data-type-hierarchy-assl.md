---
title: Hierarquia (ASSL) de tipo de dados XML de linguagem de script do Analysis Services | Microsoft Docs
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
- Analysis Services Scripting Language XML Data Type Hierarchy
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ASSL, data types
- Analysis Services Scripting Language, data types
- data types [Analysis Services Scripting Language]
- inheritance [Analysis Services Scripting Language]
- hierarchies [Analysis Services Scripting Language]
ms.assetid: f143c9f8-225d-495d-ac8e-ac2d2a7b4c07
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 2ebea80cfdecc82a3db5bb1c6cc4b10dcf40b06c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019945"
---
# <a name="analysis-services-scripting-language-xml-data-type-hierarchy-assl"></a>Hierarquia de tipos de dados XML do Analysis Services Scripting Language (ASSL)
  A tabela a seguir exibe a hierarquia de herança de tipos de dados no ASSL (Analysis Services Scripting Idioma).  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
Action  
DrillThroughAction  
ReportAction  
StandardAction  
AggregationAttribute  
AggregationDesignAttribute  
AggregationDesignDimension  
AggregationDimension  
Assembly  
ClrAssembly  
ComAssembly  
AttributeTranslation  
Binding  
AttributeBinding  
ColumnBinding  
CubeAttributeBinding  
CubeDimensionBinding  
DataSourceViewBinding  
DimensionBinding  
InheritedBinding  
MeasureBinding  
MeasureGroupBinding  
MeasureGroupDimensionBinding  
PartitionBinding  
ProactiveCachingBinding  
ProactiveCachingIncrementalProcessingBinding  
ProactiveCachingObjectNotificationBinding  
ProactiveCachingInheritedBinding  
ProactiveCachingTablesBinding  
ProactiveCachingQueryBinding  
RowBinding  
TabularBinding  
DSVTableBinding  
QueryBinding  
TableBinding  
TimeAttributeBinding  
TimeBinding  
UserDefinedGroupBinding  
ClrAssemblyFile  
CubeAttribute  
CubeBinding (out-of-line)  
CubeDimension  
CubeDimensionPermission  
CubeHierarchy  
DataBlock  
DataItem  
DataMiningMeasureGroupDimension  
DegenerateMeasureGroupDimension  
DimensionAttribute  
EventColumn  
ManyToManyMeasureGroupDimension  
MeasureGroupAttribute  
MeasureGroupBinding (out-of-line)  
MeasureGroupDimension  
MeasureGroupHierarchy  
MiningModelColumn  
MiningModelingFlag  
MiningStructureColumn  
OlapDataSource  
Permission  
PerspectiveAction  
PerspectiveAttribute  
PerspectiveCalculation  
PerspectiveDimension  
PerspectiveHierarchy  
PerspectiveKpi  
PerspectiveMeasure  
PerspectiveMeasureGroup  
PushedDataSource  
ReferenceMeasureGroupDimension  
RegularMeasureGroupDimension  
RelationalDataSource  
ScalarMiningStructureColumn  
TableMiningStructureColumn  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](data-type/analysis-services-scripting-language-xml-data-types-assl.md)   
 [Hierarquia de elemento XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-element-hierarchy-assl.md)   
 [Linguagem de script do Analysis Services &#40;ASSL&#41; referência](analysis-services-scripting-language-assl-for-xmla.md)  
  
  