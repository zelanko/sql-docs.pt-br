---
title: Elemento CalendarStartDate (ASSL) | Microsoft Docs
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
apiname: CalendarStartDate Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: CalendarStartDate
helpviewer_keywords: CalendarStartDate element
ms.assetid: f6204107-9123-41f0-acbd-52134fe36e37
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ce6b206c47856052598c5546e3fce670820decbc
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="calendarstartdate-element-assl"></a>Elemento CalendarStartDate (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Define a data de início do período de calendário para o [TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<TimeBinding>  
   ...  
   <CalendarStartDate>...</CalendarStartDate>  
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
  
 O elemento que corresponde ao pai do **CalendarStartDate** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.TimeBinding>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
