---
title: Elemento StopTime (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- StopTime Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- StopTime
helpviewer_keywords:
- StopTime element
ms.assetid: 6f863d53-033b-46e0-9837-e891e739b4b0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0970bae601d7012b01966163b84f084df4edcdfb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48108886"
---
# <a name="stoptime-element-assl"></a>Elemento StopTime (ASSL)
  Especifica a data e hora em que um [rastreamento](../objects/trace-element-assl.md) elemento deve ser interrompida.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Trace>  
   ...  
   <StopTime>...</StopTime>  
   ...  
</Trace>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|DateTime|  
|Valor padrão|None|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Rastreamento](../objects/trace-element-assl.md)|  
|Elementos filho|None|  
  
 O elemento que corresponde ao pai de `StopTime` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Trace>.  
  
## <a name="see-also"></a>Consulte também  
 [Rastreia o elemento &#40;ASSL&#41;](../collections/traces-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
