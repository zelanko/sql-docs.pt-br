---
title: Tipo de dados DataItem (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DataItem Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DataItem
helpviewer_keywords:
- DataItem data type
ms.assetid: f4f5155f-9c3d-49a1-a390-a9c734fafbce
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9f16c23941fc1048429ced974b88bba378bc72c2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48153476"
---
# <a name="dataitem-data-type-assl"></a>Tipos de dados DataItem (ASSL)
  Define um tipo de dados primitivo que representa a característica relacionada a dados de um item de dados, como, por exemplo, uma coluna ou um atributo.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DataItem>  
   <DataType>...</DataType>  
   <DataSize>...</DataSize>  
   <MimeType>...</MimeType>  
   <NullProcessing>...</NullProcessing>  
   <Trimming>...</Trimming>  
   <InvalidXmlCharacters>...</InvalidXmlCharacters>  
      <Collation>...</Collation>  
   <Format>...</Format>  
   <Source>...</Source>  
   <Annotations>...</Annotations>  
</DataItem>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|None|  
|Tipos de dados derivados|None|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|None|  
|Elementos filho|[Anotações](../collections/annotations-element-assl.md), [agrupamento](../properties/collation-element-assl.md), [DataSize](../properties/datasize-element-assl.md), [DataType](../properties/datatype-element-assl.md), [formato](../properties/format-element-assl.md), [InvalidXmlCharacters ](../properties/invalidxmlcharacters-element-assl.md), [MimeType](../properties/mimetype-element-assl.md), [NullProcessing](../properties/nullprocessing-element-assl.md), [origem](../properties/source-element-binding-assl.md), [Trimming](../properties/trimming-element-assl.md)|  
|Elementos derivados|Consulte a tabela em Comentários.|  
  
## <a name="remarks"></a>Comentários  
 O tipo de dados `DataItem` é usado para qualquer item de dado que pode ser ligado, por exemplo, a uma medida, uma chave de atributo e um nome de atributo. Os detalhes que são relevantes e os padrões que se aplicam dependem do uso; por exemplo, nomes de atributos devem ser cadeias de caracteres.  
  
 Uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] aceita apenas um determinado conjunto de tipos de dados. O uso de outros tipos de dados resulta em um erro, em vez de uma conversão implícita em um dos tipos válidos.  
  
 A tabela a seguir lista os elementos do tipo `DataItem`.  
  
|Elemento pai|Elemento do tipo `DataItem`|Comentários|  
|--------------------|----------------------------------|--------------|  
|[AttributeTranslation](../objects/column-element-assl.md)|`Source` elemento do `DataItem` deve ser do tipo [ColumnBinding](binding-data-type-assl.md) ou [AttributeBinding](attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/customrollupcolumn-element-assl.md)|`Source` elemento do `DataItem` deve ser do tipo [ColumnBinding](binding-data-type-assl.md) ou [AttributeBinding](attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/customrolluppropertiescolumn-element-assl.md)|`Source` elemento do `DataItem` deve ser do tipo [ColumnBinding](binding-data-type-assl.md) ou [AttributeBinding](attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/keycolumn-element-assl.md)|`Source` elemento do `DataItem` deve ser do tipo [ColumnBinding](binding-data-type-assl.md), [AttributeBinding](attributebinding-data-type-assl.md) ou [TimeBinding](timebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/namecolumn-element-assl.md)|`Source` elemento do `DataItem` deve ser do tipo [ColumnBinding](binding-data-type-assl.md) ou [AttributeBinding](attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/skippedlevelscolumn-element-assl.md)|`Source` elemento do `DataItem` deve ser do tipo [ColumnBinding](binding-data-type-assl.md) ou [AttributeBinding](attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/unaryoperatorcolumn-element-assl.md)|`Source` elemento do `DataItem` deve ser do tipo [ColumnBinding](binding-data-type-assl.md) ou [AttributeBinding](attributebinding-data-type-assl.md)|  
|[Medida](../objects/measure-element-assl.md)|[Origem](../properties/source-element-binding-assl.md)|`Source` elemento do `DataItem` deve ser do tipo [RowBinding](rowbinding-data-type-assl.md), [ColumnBinding](binding-data-type-assl.md), [MeasureBinding](measurebinding-data-type-assl.md), ou [CubeDimensionBinding](dimensionbinding-data-type-assl.md)|  
|[MeasureGroupAttribute](measuregroupattribute-data-type-assl.md)|[KeyColumn](../objects/keycolumn-element-assl.md)|`Source` elemento do `DataItem` deve ser do tipo [ColumnBinding](binding-data-type-assl.md), [AttributeBinding](attributebinding-data-type-assl.md) ou [InheritedBinding](inheritedbinding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](miningstructurecolumn-data-type-assl.md)|[KeyColumn](../objects/keycolumn-element-assl.md)|`Source` elemento do `DataItem` deve ser do tipo [ColumnBinding](binding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](miningstructurecolumn-data-type-assl.md)|[NameColumn](../objects/namecolumn-element-assl.md)|`Source` elemento do `DataItem` deve ser do tipo [ColumnBinding](binding-data-type-assl.md)|  
|[TableMiningStructureColumn](../objects/foreignkeycolumn-element-assl.md)|`Source` elemento do `DataItem` deve ser do tipo [ColumnBinding](binding-data-type-assl.md)|  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.DataItem>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
