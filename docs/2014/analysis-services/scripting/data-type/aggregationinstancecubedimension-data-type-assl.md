---
title: Tipo de dados AggregationInstanceCubeDimension (ASSL) | Microsoft Docs
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
- AggregationInstanceCubeDimension Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- AggregationInstanceCubeDimension data type
ms.assetid: b321ad9e-f034-4a7b-b0b7-8ba5fb162e7e
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1e6c6cc46c975eb89b1ecde559f87328005eb7a0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37237516"
---
# <a name="aggregationinstancecubedimension-data-type-assl"></a>Tipo de dados AggregationInstanceCubeDimension (ASSL)
  Define um tipo de dados primitivos que representa informações sobre uma dimensão de cubo usada por uma instância de agregação.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AggregationInstanceCubeDimension>  
   <CubeDimensionID>...</CubeDimensionID>  
   <KeyColumns>...</KeyColumns>  
   <Attributes>...</Attributes>  
</AggregationInstanceCubeDimension>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|Nenhum|  
|Tipos de dados derivados|Nenhum|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhum|  
|Elementos filho|[Attributes](../collections/attributes-element-assl.md), [CubeDimensionID](../properties/id-element-assl.md), [KeyColumns](../collections/columns-element-assl.md)|  
|Elementos derivados|[Dimension](../objects/dimension-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
