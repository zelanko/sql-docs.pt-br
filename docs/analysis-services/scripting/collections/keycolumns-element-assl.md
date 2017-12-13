---
title: Elemento KeyColumns (ASSL) | Microsoft Docs
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
apiname: KeyColumns Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: KeyColumns
helpviewer_keywords: KeyColumns element
ms.assetid: 03f3ad21-25cb-4afd-9287-cbf942ac1ad9
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0f060308e472bf290a2f04708196a5baeae797f1
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="keycolumns-element-assl"></a>Elemento KeyColumns (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém a coleção de [KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md) definições de elemento para um objeto pai.  
  
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-n: elemento obrigatório que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[AggregationInstanceAttribute](../../../analysis-services/scripting/data-type/aggregationinstanceattribute-data-type-assl.md), [AggregationInstanceCubeDimension](../../../analysis-services/scripting/data-type/aggregationinstancecubedimension-data-type-assl.md), [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md), [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|Elementos filho|[KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md) do tipo [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 O **KeyColumns** coleção pode conter vários **KeyColumn** elementos que representam um multiparte a chave para uma coluna de estrutura de mineração ou atributo.  
  
## <a name="see-also"></a>Consulte também  
 [Coleções de &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
