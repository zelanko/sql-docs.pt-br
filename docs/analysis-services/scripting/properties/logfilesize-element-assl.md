---
title: Elemento LogFileSize (ASSL) | Microsoft Docs
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
apiname: LogFileSize Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: LogFileSize
helpviewer_keywords: LogFileSize element
ms.assetid: d2135e68-57a9-4144-8403-9627041f2a58
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 09b2f3d2f613082947abf04633cc83f65a6817e3
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="logfilesize-element-assl"></a>Elemento LogFileSize (ASSL)
  Especifica o tamanho máximo de arquivo de log em megabytes.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Trace>  
  
   <LogFileSize>...</LogFileSize>  
  
</Trace>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Integer|  
|Valor padrão|**5** (megabytes)|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Rastreamento](../../../analysis-services/scripting/objects/trace-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O elemento que corresponde ao pai do **LogFileSize** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Trace>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de rastreamentos &#40; ASSL &#41;](../../../analysis-services/scripting/collections/traces-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
