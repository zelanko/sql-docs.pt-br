---
title: "Associação de tipo de dados (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Binding Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- BINDING
helpviewer_keywords:
- Binding data type
ms.assetid: 0a777219-b885-4961-ac66-b76faeb520db
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d252931193ef06109c1d353ddc8fa42b3e4b6dfb
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="binding-data-type-assl"></a>Tipo de dados Binding (ASSL)
  Define um tipo de dados primitivo abstrato que representa uma relação de dependência entre dois objetos na qual os dados ou os metadados de um objeto dependem dos dados ou metadados de um objeto associado.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Binding>...</Binding>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|Nenhuma|  
|Tipos de dados derivados|[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md), [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md), [CubeAttributeBinding](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md), [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md), [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md), [DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md), [InheritedBinding](../../../analysis-services/scripting/data-type/inheritedbinding-data-type-assl.md), [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md), [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md), [ MeasureGroupDimensionBinding](../../../analysis-services/scripting/data-type/measuregroupdimensionbinding-data-type-assl.md), [ProactiveCachingBinding](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md), [RowBinding](../../../analysis-services/scripting/data-type/rowbinding-data-type-assl.md), [TabularBinding](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md), [ TimeAttributeBinding](../../../analysis-services/scripting/data-type/timeattributebinding-data-type-assl.md), [TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md), [UserDefinedGroupBinding](../../../analysis-services/scripting/data-type/userdefinedgroupbinding-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|Nenhuma|  
|Elementos derivados|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Binding>.  
  
 Para obter mais informações sobre associação de dados, consulte [fontes de dados e associações &#40; SSAS Multidimensional &#41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="elements-of-type-binding"></a>Elementos do tipo Binding  
 A tabela a seguir lista os elementos do tipo **Binding**.  
  
|Elemento pai|Elemento do tipo **Binding**|Comentários|  
|--------------------|---------------------------------|--------------|  
|[AttributeTranslation](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)|[Origem](../../../analysis-services/scripting/properties/source-element-binding-assl.md) de [CaptionColumn](../../../analysis-services/scripting/objects/captioncolumn-element-assl.md) (do tipo [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md))|Tipo do **associação** devem ser [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md) ou [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|  
|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)|[Origem](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Tipo do **associação** devem ser [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md)|  
|[CubeBinding (fora de linha)](../../../analysis-services/scripting/data-type/cubebinding-data-type-out-of-line-assl.md)|[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|Tipo do **associação** devem ser [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|[O item de dados](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|[Origem](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|**Binding** pode ser de qualquer tipo|  
|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|[Origem](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Tipo do **associação** devem ser [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md), [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md), [DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md), ou [ TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[Origem](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Tipo do **associação** devem ser [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md) ou [UserDefinedGroupBinding](../../../analysis-services/scripting/data-type/userdefinedgroupbinding-data-type-assl.md)|  
|[DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)|[Coluna](../../../analysis-services/scripting/objects/column-element-assl.md)|Tipo do **associação** devem ser [CubeAttributeBinding](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md) ou [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|  
|[Medida](../../../analysis-services/scripting/objects/measure-element-assl.md)|[Origem](../../../analysis-services/scripting/properties/source-element-binding-assl.md) (do tipo [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md))|Tipo do **associação** devem ser [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md), [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md), [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md), ou [RowBinding](../../../analysis-services/scripting/data-type/rowbinding-data-type-assl.md)|  
|[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|[Origem](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Tipo do **associação** devem ser [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|[MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)|[Origem](../../../analysis-services/scripting/properties/source-element-binding-assl.md) de [KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md) (do tipo [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md))|Tipo do **associação** devem ser [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md) ou [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md), ou [InheritedBinding](../../../analysis-services/scripting/data-type/inheritedbinding-data-type-assl.md)|  
|[MeasureGroupBinding (fora de linha)](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|Tipo do **associação** devem ser [MeasureGroupDimensionBinding](../../../analysis-services/scripting/data-type/measuregroupdimensionbinding-data-type-assl.md)|  
|[MeasureGroupBinding (fora de linha)](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[Medida](../../../analysis-services/scripting/objects/measure-element-assl.md)|Tipo do **associação** devem ser [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|  
|[MeasureGroupBinding (fora de linha)](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[Partição](../../../analysis-services/scripting/objects/partition-element-assl.md)|Tipo do **associação** devem ser [PartitionBinding](../../../analysis-services/scripting/data-type/partitionbinding-data-type-assl.md)|  
|[MeasureGroupBinding (fora de linha)](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[Origem](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Tipo do **associação** devem ser [TableBinding](../../../analysis-services/scripting/data-type/tablebinding-data-type-assl.md)|  
|[MeasureGroupDimension](../../../analysis-services/scripting/data-type/measuregroupdimension-data-type-assl.md)|[Origem](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Tipo do **associação** devem ser [MeasureGroupDimensionBinding](../../../analysis-services/scripting/data-type/measuregroupdimensionbinding-data-type-assl.md)|  
|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|[Origem](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Tipo do **associação** devem ser [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md), [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md), ou [DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)|  
|[Partição](../../../analysis-services/scripting/objects/partition-element-assl.md)|[Origem](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Tipo do **associação** devem ser [TabularBinding](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md)|  
|[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|[Origem](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Tipo do **associação** devem ser [ProactiveCachingBinding](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|[Origem](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Tipo do **associação** devem ser [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md), [CubeAttributeBinding tipo de dados &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md), ou [tipo de dados MeasureBinding &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|  
|[TableMiningStructureColumn](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md)|[SourceMeasureGroup](../../../analysis-services/scripting/objects/sourcemeasuregroup-element-assl.md)|Tipo do **associação** devem ser [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script &#40; do Analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

