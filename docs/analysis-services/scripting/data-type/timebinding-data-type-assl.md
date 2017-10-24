---
title: Tipo de dados TimeBinding (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- TimeBinding Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TimeBinding
helpviewer_keywords:
- TimeBinding data type
ms.assetid: f3c06978-c181-4a73-9b57-8fc30358faab
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 32b8301a89ded8abbdee46941f5d905b991d14c1
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|[Associação](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
|Tipos de dados derivados|Nenhuma|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|[CalendarEndDate](../../../analysis-services/scripting/properties/calendarenddate-element-assl.md), [CalendarLanguage](../../../analysis-services/scripting/properties/calendarlanguage-element-assl.md), [CalendarStartDate](../../../analysis-services/scripting/properties/calendarstartdate-element-assl.md), [FirstDayOfWeek](../../../analysis-services/scripting/properties/firstdayofweek-element-assl.md), [FiscalFirstDayOfMonth](../../../analysis-services/scripting/properties/fiscalfirstdayofmonth-element-assl.md), [FiscalFirstMonth](../../../analysis-services/scripting/properties/fiscalfirstmonth-element-assl.md), [FiscalYearName](../../../analysis-services/scripting/properties/fiscalyearname-element-assl.md), [ManufacturingExtraMonthQuarter](../../../analysis-services/scripting/properties/manufacturingextramonthquarter-element-assl.md), [ManufacturingFirstMonth](../../../analysis-services/scripting/properties/manufacturingfirstmonth-element-assl.md), [ManufacturingFirstWeekOfMonth](../../../analysis-services/scripting/properties/manufacturingfirstweekofmonth-element-assl.md), [ReportingFirstMonth](../../../analysis-services/scripting/properties/reportingfirstmonth-element-assl.md), [ReportingFirstWeekOfMonth](../../../analysis-services/scripting/properties/reportingfirstweekofmonth-element-assl.md), [ ReportingWeekToMonthPattern](../../../analysis-services/scripting/properties/reportingweektomonthpattern-element-assl.md)|  
|Elementos derivados|Consulte [de associação](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre o **associação** tipo, incluindo tabelas de objetos do Analysis Services Scripting Language (ASSL) da **associação** tipo e a hierarquia de herança de **de associação**  tipos, consulte [associação de tipo de dados &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 Para obter uma visão geral de associações de dados em ASSL, consulte [fontes de dados e associações &#40; SSAS Multidimensional &#41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.TimeBinding>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script &#40; do Analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

