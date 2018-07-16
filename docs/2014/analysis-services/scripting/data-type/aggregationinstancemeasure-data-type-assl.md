---
title: Tipo de dados AggregationInstanceMeasure (ASSL) | Microsoft Docs
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
- AggregationInstanceMeasure Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- AggregationInstanceMeasure data type
ms.assetid: 3250970a-a67d-486c-b205-038f1bd1770f
caps.latest.revision: 10
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c8cd25248eac6ed347011db8377085cc4cd2bdd7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37263612"
---
# <a name="aggregationinstancemeasure-data-type-assl"></a>Tipo de dados AggregationInstanceMeasure (ASSL)
  Define um tipo de dados primitivo que representa informações sobre uma medida usada por uma instância de agregação.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AggregationInstanceMeasure>  
   <MeasureID>...</MeasureID>  
   <Source>...</Source>  
</AggregationInstanceMeasure>  
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
|Elementos filho|[MeasureID](../properties/id-element-assl.md), [fonte](../properties/source-element-binding-assl.md)|  
|Elementos derivados|[Medida](../objects/measure-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.AggregationInstanceMeasure>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
