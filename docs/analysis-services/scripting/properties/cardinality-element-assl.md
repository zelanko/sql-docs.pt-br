---
title: Elemento Cardinality (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Cardinality Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: Cardinality element
ms.assetid: 60ac8a26-7c8b-4011-9b9b-a29863779428
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 52dc48847eb6620431fabc5bda538a07b3235196
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="cardinality-element-assl"></a>Elemento Cardinality (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Indica a cardinalidade da relação descrita por um [AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md) ou [RegularMeasureGroupDimension](../../../analysis-services/scripting/data-type/regularmeasuregroupdimension-data-type-assl.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AttributeRelationship> <!-- or RegularMeasureGroupDimension -->  
   ...  
   <Cardinality>...</Cardinality>  
   ...  
</AttributeRelationship>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Muitos*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md), [RegularMeasureGroupDimension](../../../analysis-services/scripting/data-type/regularmeasuregroupdimension-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Muitos*|Relação muitos para um|  
|*Um*|Relação um para um|  
  
 A enumeração que corresponde aos valores permitidos para **cardinalidade** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Cardinality>.  
  
## <a name="see-also"></a>Consulte também  
 [Atributos e hierarquias de atributo](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
