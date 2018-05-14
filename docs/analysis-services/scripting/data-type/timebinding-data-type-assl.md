---
title: Tipo de dados TimeBinding (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0f97642a9b98c0fc234388d3a0baa3f6b570369b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="timebinding-data-type-assl"></a>Tipo de dados TimeBinding (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
|Elementos filho|[CalendarEndDate](../../../analysis-services/scripting/properties/calendarenddate-element-assl.md), [CalendarLanguage](../../../analysis-services/scripting/properties/calendarlanguage-element-assl.md), [CalendarStartDate](../../../analysis-services/scripting/properties/calendarstartdate-element-assl.md), [FirstDayOfWeek](../../../analysis-services/scripting/properties/firstdayofweek-element-assl.md), [FiscalFirstDayOfMonth](../../../analysis-services/scripting/properties/fiscalfirstdayofmonth-element-assl.md) , [FiscalFirstMonth](../../../analysis-services/scripting/properties/fiscalfirstmonth-element-assl.md), [FiscalYearName](../../../analysis-services/scripting/properties/fiscalyearname-element-assl.md), [ManufacturingExtraMonthQuarter](../../../analysis-services/scripting/properties/manufacturingextramonthquarter-element-assl.md), [ManufacturingFirstMonth](../../../analysis-services/scripting/properties/manufacturingfirstmonth-element-assl.md), [ManufacturingFirstWeekOfMonth](../../../analysis-services/scripting/properties/manufacturingfirstweekofmonth-element-assl.md), [ReportingFirstMonth](../../../analysis-services/scripting/properties/reportingfirstmonth-element-assl.md), [ReportingFirstWeekOfMonth](../../../analysis-services/scripting/properties/reportingfirstweekofmonth-element-assl.md), [ReportingWeekToMonthPattern](../../../analysis-services/scripting/properties/reportingweektomonthpattern-element-assl.md)|  
|Elementos derivados|Consulte [Binding](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Para obter mais informações sobre o **associação** tipo, incluindo tabelas de objetos do Analysis Services Scripting Language (ASSL) da **associação** tipo e a hierarquia de herança de **de associação**  tipos, consulte [tipo de dados de associação &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 Para obter uma visão geral de associações de dados em ASSL, consulte [fontes de dados e associações & #40; SSAS Multidimensional & #41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.TimeBinding>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script & #40; do Analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
