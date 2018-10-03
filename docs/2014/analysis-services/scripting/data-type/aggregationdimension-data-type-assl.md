---
title: Tipo de dados AggregationDimension (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AggregationDimension Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationDimension
helpviewer_keywords:
- AggregationDimension data type
ms.assetid: 697e0e09-3210-4a56-882f-80726abc4c68
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 325c6bf84127c060be132ce44107220077e215c4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48094987"
---
# <a name="aggregationdimension-data-type-assl"></a>Tipo de dados AggregationDimension (ASSL)
  Define um tipo de dados primitivo que representa a relação entre uma dimensão e um [agregação](../objects/aggregation-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AggregationDimension>  
   <CubeDimensionID>...</CubeDimensionID>  
   <Attributes>...</Attributes>  
      <Annotations>...</Annotations>  
</AggregationDimension>  
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
|Elementos filho|[Anotações](../collections/annotations-element-assl.md), [atributos](../collections/attributes-element-assl.md), [CubeDimensionID](../properties/id-element-assl.md)|  
|Elementos derivados|[Dimensão](../objects/dimension-element-assl.md) ([dimensões](../collections/dimensions-element-assl.md) coleção de [agregação](../objects/aggregation-element-assl.md))|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é [AggregationDimension](dimension-data-type-assl.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
