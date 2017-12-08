---
title: Elemento CalendarEndDate (ASSL) | Microsoft Docs
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
apiname: CalendarEndDate Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: CalendarEndDate
helpviewer_keywords: CalendarEndDate element
ms.assetid: abedd074-9a28-4169-85b5-49ea57f10fb6
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 82b97e05267c879ba949a66453a4295b015449d8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="calendarenddate-element-assl"></a>Elemento CalendarEndDate (ASSL)
  Define a data de término do período de calendário para um [TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<TimeBinding>  
   ...  
   <CalendarEndDate>...</CalendarEndDate>  
   ...  
</TimeBinding>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|DateTime|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O **CalendarEndDate** deve ficar depois o **CalendarStartDate**.  
  
 O elemento que corresponde ao pai do **CalendarEndDate** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.TimeBinding>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
