---
title: Elemento LogFileRollover (ASSL) | Microsoft Docs
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
apiname: LogFileRollover Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: LogFileRollover
helpviewer_keywords: LogFileRollover element
ms.assetid: 5484e167-b891-431a-bbae-946ea6eb4a3c
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 904da9adc727b93c89bc5f2a5e9adaea78735788
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="logfilerollover-element-assl"></a>Elemento LogFileRollover (ASSL)
  Especifica se o registro de [rastreamento](../../../analysis-services/scripting/objects/trace-element-assl.md) saída deve passar para um novo arquivo ou deve parar quando o arquivo de log máximo tamanho especificado em [LogFileSize](../../../analysis-services/scripting/properties/logfilesize-element-assl.md) for atingido.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Trace>  
   ...  
   <LogFileRollover>...</LogFileRollover>  
   ...  
</Trace>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Boolean|  
|Valor padrão|False|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Rastreamento](../../../analysis-services/scripting/objects/trace-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Se o valor do elemento **LogFileRollover** for definido como True, um novo arquivo será iniciado quando o tamanho do arquivo de log excede o valor especificado no elemento **LogFileSize** do elemento pai **Trace** ; caso contrário, o registro para.  
  
 O elemento que corresponde ao pai do **LogFileRollover** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Trace>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de rastreamentos &#40; ASSL &#41;](../../../analysis-services/scripting/collections/traces-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
