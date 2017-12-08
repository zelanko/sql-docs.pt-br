---
title: Elemento FirstDayOfWeek (ASSL) | Microsoft Docs
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
apiname: FirstDayOfWeek Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: FirstDayOfWeek
helpviewer_keywords: FirstDayOfWeek element
ms.assetid: d3c92fa3-b293-43b5-806e-cd1c146a3a7c
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fb6949a52800150ec90e47e2c0bf4b2deaeed605
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="firstdayofweek-element-assl"></a>Elemento FirstDayOfWeek (ASSL)
  Define o primeiro dia da semana para um [TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<TimeBinding>  
   ...  
   <FirstDayOfWeek>...</FirstDayOfWeek>  
   ...  
</TimeBinding>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Inteiro (entre 1 e 7, sendo que 1 = domingo e 7 = sábado)|  
|Valor padrão|**1**|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O elemento que corresponde ao pai do **FirstDayOfWeek** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.TimeBinding>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
