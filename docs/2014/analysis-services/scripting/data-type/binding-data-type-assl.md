---
title: Associação de tipo de dados (ASSL) | Microsoft Docs
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
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 24847c70a0baf6ee12c1de6364cdd1e8d4327f91
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119208"
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
|Tipos de dados base|Nenhum|  
|Tipos de dados derivados|[AttributeBinding](binding-data-type-assl.md), [ColumnBinding](columnbinding-data-type-assl.md), [CubeAttributeBinding](cubeattributebinding-data-type-assl.md), [CubeDimensionBinding](dimensionbinding-data-type-assl.md), [DataSourceViewBinding](datasourceviewbinding-data-type-assl.md), [DimensionBinding](dimensionbinding-data-type-assl.md), [InheritedBinding](inheritedbinding-data-type-assl.md), [MeasureBinding](measurebinding-data-type-assl.md), [MeasureGroupBinding](measuregroupbinding-data-type-assl.md), [MeasureGroupDimensionBinding](measuregroupdimensionbinding-data-type-assl.md), [ProactiveCachingBinding](proactivecachingbinding-data-type-assl.md), [RowBinding](rowbinding-data-type-assl.md), [TabularBinding](tabularbinding-data-type-assl.md), [TimeAttributeBinding](timeattributebinding-data-type-assl.md), [TimeBinding](timebinding-data-type-assl.md), [UserDefinedGroupBinding](userdefinedgroupbinding-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhum|  
|Elementos filho|Nenhum|  
|Elementos derivados|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Binding>.  
  
 Para obter mais informações sobre associação de dados, consulte [fontes de dados e associações &#40;multidimensionais do SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="elements-of-type-binding"></a>Elementos do tipo Binding  
 A tabela a seguir lista os elementos do tipo `Binding`.  
  
|Elemento pai|Elemento do tipo `Binding`|Comentários|  
|--------------------|---------------------------------|--------------|  
|[AttributeTranslation](../properties/source-element-binding-assl.md) de [CaptionColumn](../objects/column-element-assl.md) (do tipo [DataItem](dataitem-data-type-assl.md))|Tipo do `Binding` devem ser [AttributeBinding](binding-data-type-assl.md) ou [ColumnBinding](columnbinding-data-type-assl.md)|  
|[Cube](../objects/cube-element-assl.md)|[Origem](../properties/source-element-binding-assl.md)|Tipo do `Binding` devem ser [DataSourceViewBinding](datasourceviewbinding-data-type-assl.md)|  
|[CubeBinding (fora de linha)](../objects/group-element-assl.md)|Tipo do `Binding` devem ser [MeasureGroupBinding](measuregroupbinding-data-type-assl.md)|  
|[O item de dados](dataitem-data-type-assl.md)|[Origem](../properties/source-element-binding-assl.md)|`Binding` pode ser de qualquer tipo|  
|[Dimension](../objects/dimension-element-assl.md)|[Origem](../properties/source-element-binding-assl.md)|Tipo do `Binding` devem ser [CubeDimensionBinding](dimensionbinding-data-type-assl.md), [DataSourceViewBinding](datasourceviewbinding-data-type-assl.md), [DimensionBinding](dimensionbinding-data-type-assl.md), ou [TimeBinding](timebinding-data-type-assl.md)|  
|[DimensionAttribute](dimensionattribute-data-type-assl.md)|[Origem](../properties/source-element-binding-assl.md)|Tipo do `Binding` devem ser [AttributeBinding](binding-data-type-assl.md) ou [UserDefinedGroupBinding](userdefinedgroupbinding-data-type-assl.md)|  
|[DrillThroughAction](action-data-type-assl.md)|[Coluna](../objects/column-element-assl.md)|Tipo do `Binding` devem ser [CubeAttributeBinding](cubeattributebinding-data-type-assl.md) ou [MeasureBinding](measurebinding-data-type-assl.md)|  
|[Medida](../objects/measure-element-assl.md)|[Origem](../properties/source-element-binding-assl.md) (do tipo [DataItem](dataitem-data-type-assl.md))|Tipo do `Binding` devem ser [ColumnBinding](columnbinding-data-type-assl.md), [CubeDimensionBinding](dimensionbinding-data-type-assl.md), [MeasureBinding](measurebinding-data-type-assl.md), ou [RowBinding](rowbinding-data-type-assl.md)|  
|[MeasureGroup](../objects/measuregroup-element-assl.md)|[Origem](../properties/source-element-binding-assl.md)|Tipo do `Binding` devem ser [MeasureGroupBinding](measuregroupbinding-data-type-assl.md)|  
|[MeasureGroupAttribute](measuregroupattribute-data-type-assl.md)|[Origem](../properties/source-element-binding-assl.md) de [KeyColumn](../objects/keycolumn-element-assl.md) (do tipo [DataItem](dataitem-data-type-assl.md))|Tipo do `Binding` devem ser [AttributeBinding](binding-data-type-assl.md) ou [ColumnBinding](columnbinding-data-type-assl.md), ou [InheritedBinding](inheritedbinding-data-type-assl.md)|  
|[MeasureGroupBinding (fora de linha)](measuregroupbinding-data-type-out-of-line-assl.md)|[Dimension](../objects/dimension-element-assl.md)|Tipo do `Binding` devem ser [MeasureGroupDimensionBinding](measuregroupdimensionbinding-data-type-assl.md)|  
|[MeasureGroupBinding (fora de linha)](measuregroupbinding-data-type-out-of-line-assl.md)|[Medida](../objects/measure-element-assl.md)|Tipo do `Binding` devem ser [MeasureBinding](measurebinding-data-type-assl.md)|  
|[MeasureGroupBinding (fora de linha)](../objects/partition-element-assl.md)|Tipo do `Binding` devem ser [PartitionBinding](partitionbinding-data-type-assl.md)|  
|[MeasureGroupBinding (fora de linha)](measuregroupbinding-data-type-out-of-line-assl.md)|[Origem](../properties/source-element-binding-assl.md)|Tipo do `Binding` devem ser [TableBinding](tablebinding-data-type-assl.md)|  
|[MeasureGroupDimension](dimension-data-type-assl.md)|[Origem](../properties/source-element-binding-assl.md)|Tipo do `Binding` devem ser [MeasureGroupDimensionBinding](measuregroupdimensionbinding-data-type-assl.md)|  
|[MiningStructure](../objects/miningstructure-element-assl.md)|[Origem](../properties/source-element-binding-assl.md)|Tipo do `Binding` devem ser [CubeDimensionBinding](dimensionbinding-data-type-assl.md), [DataSourceViewBinding](datasourceviewbinding-data-type-assl.md), ou [DimensionBinding](dimensionbinding-data-type-assl.md)|  
|[Partição](../objects/partition-element-assl.md)|[Origem](../properties/source-element-binding-assl.md)|Tipo do `Binding` devem ser [TabularBinding](tabularbinding-data-type-assl.md)|  
|[ProactiveCaching](../objects/proactivecaching-element-assl.md)|[Origem](../properties/source-element-binding-assl.md)|Tipo do `Binding` devem ser [ProactiveCachingBinding](proactivecachingbinding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](miningstructurecolumn-data-type-assl.md)|[Origem](../properties/source-element-binding-assl.md)|Tipo do `Binding` devem ser [AttributeBinding](binding-data-type-assl.md), [tipo de dados CubeAttributeBinding &#40;ASSL&#41;](cubeattributebinding-data-type-assl.md), ou [o tipo de dados MeasureBinding &#40;ASSL&#41;](measurebinding-data-type-assl.md)|  
|[TableMiningStructureColumn](../objects/sourcemeasuregroup-element-assl.md)|Tipo do `Binding` devem ser [MeasureGroupBinding](measuregroupbinding-data-type-assl.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  