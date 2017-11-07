---
title: Tipo de elemento (MeasureGroupAttribute) (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Type Element (MeasureGroupAttribute)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: 93740504-297a-4a06-ab3e-b598e466eebb
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 966c5e29b9f6f2569260ea90dd32f76cab4b064d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="type-element-measuregroupattribute-assl"></a>Elemento Type (MeasureGroupAttribute) (ASSL)
  Contém o tipo de um [MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MeasureGroupAttribute>  
   ...  
   <Type>...</Type>  
   ...  
</MeasureGroupAttribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Regular*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Regular*|Representa um atributo regular.|  
|*Granularidade*|Representa um atributo de granularidade.|  
  
 A enumeração que corresponde aos valores permitidos para **tipo** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MeasureGroupAttributeType>.  
  
 O elemento que corresponde ao pai do **tipo** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MeasureGroupAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Atributos de elemento &#40; ASSL &#41;](../../../analysis-services/scripting/collections/attributes-element-assl.md)   
 [Tipo de dados RegularMeasureGroupDimension &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/regularmeasuregroupdimension-data-type-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

