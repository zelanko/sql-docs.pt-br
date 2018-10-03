---
title: Tipo de dados AggregationInstanceAttribute (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AggregationInstanceAttribute Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- AggregationInstanceAttribute data type
ms.assetid: fc5a98bf-7c3c-4faf-b9f8-16eb073d7dc7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9bd2bb1b8db7b9913c516dc5b3801e694aebafaf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219366"
---
# <a name="aggregationinstanceattribute-data-type-assl"></a>Tipo de dados AggregationInstanceAttribute (ASSL)
  Define um tipo de dados primitivos que representa informações sobre um atributo usado por uma instância de agregação.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AggregationInstanceAttribute>  
   <AttributeID>...</AttributeID>  
   <KeyColumns>...</KeyColumns>  
</AggregationInstanceAttribute>  
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
|Elementos filho|[AttributeID](../properties/id-element-assl.md), [KeyColumns](../collections/columns-element-assl.md)|  
|Elementos derivados|[Atributo](../objects/attribute-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.AggregationInstanceAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
