---
title: Elemento KeyColumns (ASSL) | Microsoft Docs
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
- KeyColumns Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- KeyColumns
helpviewer_keywords:
- KeyColumns element
ms.assetid: 03f3ad21-25cb-4afd-9287-cbf942ac1ad9
caps.latest.revision: 32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 88df5fa8590bf3f049632abb8137e62e959a67fe
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37151607"
---
# <a name="keycolumns-element-assl"></a>Elemento KeyColumns (ASSL)
  Contém a coleção de [KeyColumn](../objects/column-element-assl.md) definições de elemento para um objeto pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttribute> <!-- or AggregationInstanceAttribute, AggregationInstanceCubeDimension, MeasureGroupAttribute, ScalarMiningStructureColumn -->  
   ...  
   <KeyColumns>  
      <KeyColumn xsi:type="DataItem"...</KeyColumn>  
   </KeyColumns>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-n: elemento obrigatório que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[AggregationInstanceAttribute](../data-type/aggregationinstanceattribute-data-type-assl.md), [AggregationInstanceCubeDimension](../data-type/dimension-data-type-assl.md), [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md), [MeasureGroupAttribute](../data-type/measuregroupattribute-data-type-assl.md), [ ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|Elementos filho|[KeyColumn](../objects/column-element-assl.md) do tipo [DataItem](../data-type/dataitem-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 A coleção `KeyColumns` pode conter vários elementos `KeyColumn` que representam uma chave de várias partes para uma coluna de atributo ou estrutura de mineração.  
  
## <a name="see-also"></a>Consulte também  
 [Coleções &#40;ASSL&#41;](collections-assl.md)  
  
  
