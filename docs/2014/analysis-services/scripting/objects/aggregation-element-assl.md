---
title: Elemento Aggregation (ASSL) | Microsoft Docs
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
- Aggregation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Aggregation
helpviewer_keywords:
- Aggregation element
ms.assetid: f37af388-b2b3-4234-a1d6-936ee9b7f2ae
caps.latest.revision: 39
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 51e28a8435b2891cf623ea851824809606d83620
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37157187"
---
# <a name="aggregation-element-assl"></a>Elemento Aggregation (ASSL)
  Define uma única agregação para um [partição](partition-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Aggregations>  
      <Aggregation>  
      <ID>...</ID>  
      <Name>...</Name>  
      <Dimensions>...</Dimensions>  
            <Annotations>...</Annotations>  
      <Description>...</Description>  
   </Aggregation>  
</Aggregations>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Agregações](../collections/aggregations-element-assl.md)|  
|Elementos filho|[Anotações](../collections/annotations-element-assl.md), [descrição](../properties/description-element-assl.md), [dimensões](../collections/dimensions-element-assl.md), [ID](../properties/id-element-assl.md), [nome](../properties/name-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Aggregation>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de partição &#40;ASSL&#41;](partition-element-assl.md)   
 [Elemento AggregationDesign &#40;ASSL&#41;](aggregationdesign-element-assl.md)   
 [Elemento MeasureGroup &#40;ASSL&#41;](group-element-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
