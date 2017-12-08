---
title: Elemento ReportingWeekToMonthPattern (ASSL) | Microsoft Docs
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
apiname: ReportingWeekToMonthPattern Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ReportingWeekToMonthPattern
helpviewer_keywords: ReportingWeekToMonthPattern element
ms.assetid: 8d7c694d-d5c5-4faa-af78-155779e84fe9
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c0996d1a364b237d2004f37fd1a85bd84d076522
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="reportingweektomonthpattern-element-assl"></a>Elemento ReportingWeekToMonthPattern (ASSL)
  Define o padrão de semana a mês de relatório para o [TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<TimeBinding>  
   ...  
   <ReportingWeekToMonthPattern>...</ReportingWeekToMonthPattern>  
   ...  
</TimeBinding>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*445*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*445*|Quatro semanas no primeiro mês do trimestre, quatro semanas no segundo mês e cinco semanas no terceiro mês.|  
|*454*|Quatro semanas no primeiro mês do trimestre, cinco semanas no segundo mês e quatro semanas no terceiro mês.|  
|*544*|Cinco semanas no primeiro mês do trimestre, quatro semanas no segundo mês e quatro semanas no terceiro mês.|  
  
 A enumeração que corresponde aos valores permitidos para **ReportingWeekToMonthPattern** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ReportingWeekToMonthPattern>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
