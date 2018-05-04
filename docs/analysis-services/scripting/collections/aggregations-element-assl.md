---
title: Elemento Aggregations (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Aggregations Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Aggregations
helpviewer_keywords:
- Aggregations element
ms.assetid: 79b7de7a-53b2-4202-bc0f-de1daaf1b179
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d4de0c42e0f03a1539aab76f82a2bcc0a5c860d2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="aggregations-element-assl"></a>Elemento Aggregations (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contém a coleção de agregações definida para um [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AggregationDesign>  
   ...  
   <Aggregations>  
      <Aggregation>...</Aggregation>  
   </Aggregations>  
   ...  
</AggregationDimension>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum (coleção)|  
|Valor padrão|Nenhum (coleção)|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)|  
|Elementos filho|[Agregação](../../../analysis-services/scripting/objects/aggregation-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.AggregationCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento MeasureGroup &#40;ASSL&#41;](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)   
 [Elemento de partição &#40;ASSL&#41;](../../../analysis-services/scripting/objects/partition-element-assl.md)   
 [Coleções de & #40; ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
