---
title: Elemento ColumnID (EventColumn) (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ColumnID Element (EventColumn)
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ColumnID
helpviewer_keywords: ColumnID element
ms.assetid: c4f4fbad-9d70-4de2-8cf7-caee80a4a1e4
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 068aee390a3208b55323b31720bb42eeaa39f7d8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="columnid-element-eventcolumn-assl"></a>Elemento ColumnID (EventColumn) (ASSL)
  Contém o identificador (ID) da coluna de informações a serem capturadas para um evento como parte de um [rastreamento](../../../analysis-services/scripting/objects/trace-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<EventColumn>  
   <ColumnID>...</ColumnID>  
</EventColumn>  
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
|Elemento pai|[EventColumn](../../../analysis-services/scripting/data-type/eventcolumn-data-type-assl.md)|  
|Elementos filho|Nenhum.|  
  
## <a name="remarks"></a>Comentários  
 O elemento que corresponde ao pai do **ColumnID** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.TraceColumn>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de colunas &#40; ASSL &#41;](../../../analysis-services/scripting/collections/columns-element-assl.md)   
 [Elemento Event &#40; ASSL &#41;](../../../analysis-services/scripting/objects/event-element-assl.md)   
 [Elemento de eventos &#40; ASSL &#41;](../../../analysis-services/scripting/collections/events-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
