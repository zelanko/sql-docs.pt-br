---
title: Elemento Cardinality (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Cardinality Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Cardinality element
ms.assetid: 60ac8a26-7c8b-4011-9b9b-a29863779428
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7446923efc15a2fe05f3e8bf8c86a2e9f429a2c1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37325076"
---
# <a name="cardinality-element-assl"></a>Elemento Cardinality (ASSL)
  Indica a cardinalidade da relação descrita por um [AttributeRelationship](../objects/attributerelationship-element-assl.md) ou [RegularMeasureGroupDimension](../data-type/dimension-data-type-assl.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AttributeRelationship> <!-- or RegularMeasureGroupDimension -->  
   ...  
   <Cardinality>...</Cardinality>  
   ...  
</AttributeRelationship>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Muitos*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[AttributeRelationship](../objects/attributerelationship-element-assl.md), [RegularMeasureGroupDimension](../data-type/dimension-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Muitos*|Relação muitos para um|  
|*Um*|Relação um para um|  
  
 A enumeração que corresponde aos valores permitidos para `Cardinality` no modelo de objeto AMO (Objetos de Gerenciamento de Análise) é <xref:Microsoft.AnalysisServices.Cardinality>.  
  
## <a name="see-also"></a>Consulte também  
 [Atributos e hierarquias de atributo](../../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
