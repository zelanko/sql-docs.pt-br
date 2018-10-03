---
title: Elemento OrderByAttributeID (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- OrderByAttributeID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- OrderByAttributeID
helpviewer_keywords:
- OrderByAttributeID element
ms.assetid: 41d7b650-ac40-4f1a-850d-2f81a19b28cb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 57527661434149652c0c0b70f12a53803247d2f6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48103416"
---
# <a name="orderbyattributeid-element-assl"></a>Elemento OrderByAttributeID (ASSL)
  Identifica outro atributo pelo qual ordenar os membros de [dimensão](../data-type/dimensionattribute-data-type-assl.md) atributo.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttribute>  
   ...  
      <OrderByAttributeID>...</OrderByAttributeID>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|None|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O `OrderByAttributeID` elemento é usado apenas quando o valor da [OrderBy](orderby-element-assl.md) elemento para o `DimensionAttribute` está definido como *AttributeKey* ou *AttributeName*.  
  
 O elemento que corresponde ao pai de `OrderByAttributeID` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
