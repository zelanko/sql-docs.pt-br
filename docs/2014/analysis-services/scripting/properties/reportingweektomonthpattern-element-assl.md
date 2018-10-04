---
title: Elemento ReportingWeekToMonthPattern (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ReportingWeekToMonthPattern Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ReportingWeekToMonthPattern
helpviewer_keywords:
- ReportingWeekToMonthPattern element
ms.assetid: 8d7c694d-d5c5-4faa-af78-155779e84fe9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 61667552266673b71bae7b8046e47d6c4db5c9f1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48083416"
---
# <a name="reportingweektomonthpattern-element-assl"></a>Elemento ReportingWeekToMonthPattern (ASSL)
  Define o padrão de semana-para-mês de relatório para o [TimeBinding](../data-type/binding-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<TimeBinding>  
   ...  
   <ReportingWeekToMonthPattern>...</ReportingWeekToMonthPattern>  
   ...  
</TimeBinding>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*445*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[TimeBinding](../data-type/binding-data-type-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*445*|Quatro semanas no primeiro mês do trimestre, quatro semanas no segundo mês e cinco semanas no terceiro mês.|  
|*454*|Quatro semanas no primeiro mês do trimestre, cinco semanas no segundo mês e quatro semanas no terceiro mês.|  
|*544*|Cinco semanas no primeiro mês do trimestre, quatro semanas no segundo mês e quatro semanas no terceiro mês.|  
  
 A enumeração que corresponde aos valores permitidos para `ReportingWeekToMonthPattern` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ReportingWeekToMonthPattern>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
