---
title: Tipo de dados TimeBinding (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- TimeBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TimeBinding
helpviewer_keywords:
- TimeBinding data type
ms.assetid: f3c06978-c181-4a73-9b57-8fc30358faab
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d5d8b1ea5b0b7350fdba80d5ea99b7f3c0cc9ee1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48095576"
---
# <a name="timebinding-data-type-assl"></a>Tipo de dados TimeBinding (ASSL)
  Define um tipo de dados derivado que representa uma associação aos períodos de tempo.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<TimeBinding>  
   <!-- The following elements extend Binding -->  
      <CalendarStartDate>...</CalendarStartDate>  
      <CalendarEndDate>...</CalendarEndDate>  
      <FirstDayOfWeek>...</FirstDayOfWeek>  
   <CalendarLanguage>...</CalendarLanguage>  
   <FiscalFirstMonth>...</FiscalFirstMonth>  
   <FiscalFirstDayOfMonth>...</FiscalFirstDayOfMonth>  
   <FiscalYearName>...</FiscalYearName>  
   <ReportingFirstMonth>...</ReportingFirstMonth>  
   <ReportingFirstWeekOfMonth>...</ReportingFirstWeekOfMonth>  
   <ReportingWeekToMonthPattern>...</ReportingWeekToMonthPattern>  
   <ManufacturingFirstMonth>...</ManufacturingFirstMonth>  
   <ManufacturingFirstWeekOfMonth>...</ManufacturingFirstWeekOfMonth>  
   <ManufacturingExtraMonthQuarter>...</ManufacturingExtraMonthQuarter>  
</TimeBinding>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|[Associação](binding-data-type-assl.md)|  
|Tipos de dados derivados|None|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|None|  
|Elementos filho|[CalendarEndDate](../properties/calendarenddate-element-assl.md), [CalendarLanguage](../properties/language-element-assl.md), [CalendarStartDate](../properties/calendarstartdate-element-assl.md), [FirstDayOfWeek](../properties/firstdayofweek-element-assl.md), [FiscalFirstDayOfMonth](../properties/fiscalfirstdayofmonth-element-assl.md) , [FiscalFirstMonth](../properties/fiscalfirstmonth-element-assl.md), [FiscalYearName](../properties/name-element-assl.md), [ManufacturingExtraMonthQuarter](../properties/manufacturingextramonthquarter-element-assl.md), [ManufacturingFirstMonth](../properties/manufacturingfirstmonth-element-assl.md), [ManufacturingFirstWeekOfMonth](../properties/manufacturingfirstweekofmonth-element-assl.md), [ReportingFirstMonth](../properties/reportingfirstmonth-element-assl.md), [ReportingFirstWeekOfMonth](../properties/reportingfirstweekofmonth-element-assl.md), [ReportingWeekToMonthPattern](../properties/reportingweektomonthpattern-element-assl.md)|  
|Elementos derivados|Consulte [de associação](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre o `Binding` tipo, incluindo tabelas de objetos do Analysis Services Scripting Language (ASSL) da `Binding` tipo e a hierarquia de herança dos `Binding` tipos, consulte [tipo de associação de dados &#40;ASSL &#41;](binding-data-type-assl.md).  
  
 Para uma visão geral de associações de dados em ASSL, consulte [fontes de dados e associações &#40;Multidimensional do SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.TimeBinding>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
