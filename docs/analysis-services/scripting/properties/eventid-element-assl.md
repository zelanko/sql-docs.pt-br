---
title: Elemento EventID (ASSL) | Microsoft Docs
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
apiname: EventID Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: EventID
helpviewer_keywords: EventID element
ms.assetid: a6b2ee50-1753-496c-af5c-206d63f2542b
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 84c93d7de8ff1d1761b5d818f046cb8e69a0ca71
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="eventid-element-assl"></a>Elemento EventID (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Identifica exclusivamente um [evento](../../../analysis-services/scripting/objects/event-element-assl.md) elemento que será capturado como parte de um [rastreamento](../../../analysis-services/scripting/objects/trace-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Event>  
  
      <EventID>...</EventID>  
  
</Event>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Evento](../../../analysis-services/scripting/objects/event-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente para o pai do **EventID** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.TraceEvent>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de eventos &#40; ASSL &#41;](../../../analysis-services/scripting/collections/events-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
