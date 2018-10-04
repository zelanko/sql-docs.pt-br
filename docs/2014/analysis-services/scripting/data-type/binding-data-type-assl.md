---
title: Associação de tipo de dados (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Binding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- BINDING
helpviewer_keywords:
- Binding data type
ms.assetid: 0a777219-b885-4961-ac66-b76faeb520db
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2e46d48f94035a59c54a3e9bb9c8ccb087226660
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48135896"
---
# <a name="binding-data-type-assl"></a>Tipo de dados Binding (ASSL)
  Define um tipo de dados primitivo abstrato que representa uma relação de dependência entre dois objetos na qual os dados ou os metadados de um objeto dependem dos dados ou metadados de um objeto associado.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Binding>...</Binding>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|None|  
|Tipos de dados derivados|[AttributeBinding](binding-data-type-assl.md), [ColumnBinding](columnbinding-data-type-assl.md), [CubeAttributeBinding](cubeattributebinding-data-type-assl.md), [CubeDimensionBinding](dimensionbinding-data-type-assl.md), [DataSourceViewBinding](datasourceviewbinding-data-type-assl.md), [DimensionBinding](dimensionbinding-data-type-assl.md), [InheritedBinding](inheritedbinding-data-type-assl.md), [MeasureBinding](measurebinding-data-type-assl.md), [MeasureGroupBinding](measuregroupbinding-data-type-assl.md), [ MeasureGroupDimensionBinding](measuregroupdimensionbinding-data-type-assl.md), [ProactiveCachingBinding](proactivecachingbinding-data-type-assl.md), [RowBinding](rowbinding-data-type-assl.md), [TabularBinding](tabularbinding-data-type-assl.md), [ TimeAttributeBinding](timeattributebinding-data-type-assl.md), [TimeBinding](timebinding-data-type-assl.md), [UserDefinedGroupBinding](userdefinedgroupbinding-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|None|  
|Elementos filho|None|  
|Elementos derivados|None|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Binding>.  
  
 Para obter mais informações sobre associação de dados, consulte [fontes de dados e associações &#40;Multidimensional do SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="elements-of-type-binding"></a>Elementos do tipo Binding  
 A tabela a seguir lista os elementos do tipo `Binding`.  
  
|Elemento pai|Elemento do tipo `Binding`|Comentários|  
|--------------------|---------------------------------|--------------|  
|[AttributeTranslation](../properties/source-element-binding-assl.md) dos [CaptionColumn](../objects/column-element-assl.md) (do tipo [DataItem](dataitem-data-type-assl.md))|Tipo dos `Binding` deve ser [AttributeBinding](binding-data-type-assl.md) ou [ColumnBinding](columnbinding-data-type-assl.md)|  
|[Cube](../objects/cube-element-assl.md)|[Origem](../properties/source-element-binding-assl.md)|Tipo dos `Binding` deve ser [DataSourceViewBinding](datasourceviewbinding-data-type-assl.md)|  
|[CubeBinding (fora de linha)](../objects/group-element-assl.md)|Tipo dos `Binding` deve ser [MeasureGroupBinding](measuregroupbinding-data-type-assl.md)|  
|[DataItem](dataitem-data-type-assl.md)|[Origem](../properties/source-element-binding-assl.md)|`Binding` pode ser de qualquer tipo|  
|[Dimension](../objects/dimension-element-assl.md)|[Origem](../properties/source-element-binding-assl.md)|Tipo dos `Binding` deve ser [CubeDimensionBinding](dimensionbinding-data-type-assl.md), [DataSourceViewBinding](datasourceviewbinding-data-type-assl.md), [DimensionBinding](dimensionbinding-data-type-assl.md), ou [TimeBinding](timebinding-data-type-assl.md)|  
|[DimensionAttribute](dimensionattribute-data-type-assl.md)|[Origem](../properties/source-element-binding-assl.md)|Tipo dos `Binding` deve ser [AttributeBinding](binding-data-type-assl.md) ou [UserDefinedGroupBinding](userdefinedgroupbinding-data-type-assl.md)|  
|[DrillThroughAction](action-data-type-assl.md)|[Coluna](../objects/column-element-assl.md)|Tipo dos `Binding` deve ser [CubeAttributeBinding](cubeattributebinding-data-type-assl.md) ou [MeasureBinding](measurebinding-data-type-assl.md)|  
|[Medida](../objects/measure-element-assl.md)|[Código-fonte](../properties/source-element-binding-assl.md) (do tipo [DataItem](dataitem-data-type-assl.md))|Tipo dos `Binding` deve ser [ColumnBinding](columnbinding-data-type-assl.md), [CubeDimensionBinding](dimensionbinding-data-type-assl.md), [MeasureBinding](measurebinding-data-type-assl.md), ou [RowBinding](rowbinding-data-type-assl.md)|  
|[MeasureGroup](../objects/measuregroup-element-assl.md)|[Origem](../properties/source-element-binding-assl.md)|Tipo dos `Binding` deve ser [MeasureGroupBinding](measuregroupbinding-data-type-assl.md)|  
|[MeasureGroupAttribute](measuregroupattribute-data-type-assl.md)|[Código-fonte](../properties/source-element-binding-assl.md) dos [KeyColumn](../objects/keycolumn-element-assl.md) (do tipo [DataItem](dataitem-data-type-assl.md))|Tipo dos `Binding` deve ser [AttributeBinding](binding-data-type-assl.md) ou [ColumnBinding](columnbinding-data-type-assl.md), ou [InheritedBinding](inheritedbinding-data-type-assl.md)|  
|[MeasureGroupBinding (fora de linha)](measuregroupbinding-data-type-out-of-line-assl.md)|[Dimension](../objects/dimension-element-assl.md)|Tipo dos `Binding` deve ser [MeasureGroupDimensionBinding](measuregroupdimensionbinding-data-type-assl.md)|  
|[MeasureGroupBinding (fora de linha)](measuregroupbinding-data-type-out-of-line-assl.md)|[Medida](../objects/measure-element-assl.md)|Tipo dos `Binding` deve ser [MeasureBinding](measurebinding-data-type-assl.md)|  
|[MeasureGroupBinding (fora de linha)](../objects/partition-element-assl.md)|Tipo dos `Binding` deve ser [PartitionBinding](partitionbinding-data-type-assl.md)|  
|[MeasureGroupBinding (fora de linha)](measuregroupbinding-data-type-out-of-line-assl.md)|[Origem](../properties/source-element-binding-assl.md)|Tipo dos `Binding` deve ser [TableBinding](tablebinding-data-type-assl.md)|  
|[MeasureGroupDimension](dimension-data-type-assl.md)|[Origem](../properties/source-element-binding-assl.md)|Tipo dos `Binding` deve ser [MeasureGroupDimensionBinding](measuregroupdimensionbinding-data-type-assl.md)|  
|[MiningStructure](../objects/miningstructure-element-assl.md)|[Origem](../properties/source-element-binding-assl.md)|Tipo dos `Binding` deve ser [CubeDimensionBinding](dimensionbinding-data-type-assl.md), [DataSourceViewBinding](datasourceviewbinding-data-type-assl.md), ou [DimensionBinding](dimensionbinding-data-type-assl.md)|  
|[Partição](../objects/partition-element-assl.md)|[Origem](../properties/source-element-binding-assl.md)|Tipo dos `Binding` deve ser [TabularBinding](tabularbinding-data-type-assl.md)|  
|[ProactiveCaching](../objects/proactivecaching-element-assl.md)|[Origem](../properties/source-element-binding-assl.md)|Tipo dos `Binding` deve ser [ProactiveCachingBinding](proactivecachingbinding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](miningstructurecolumn-data-type-assl.md)|[Origem](../properties/source-element-binding-assl.md)|Tipo dos `Binding` deve ser [AttributeBinding](binding-data-type-assl.md), [tipo de dados CubeAttributeBinding &#40;ASSL&#41;](cubeattributebinding-data-type-assl.md), ou [tipo de dados MeasureBinding &#40;ASSL&#41;](measurebinding-data-type-assl.md)|  
|[TableMiningStructureColumn](../objects/sourcemeasuregroup-element-assl.md)|Tipo dos `Binding` deve ser [MeasureGroupBinding](measuregroupbinding-data-type-assl.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
