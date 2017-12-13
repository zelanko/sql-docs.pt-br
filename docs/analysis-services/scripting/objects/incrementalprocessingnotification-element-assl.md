---
title: Elemento IncrementalProcessingNotification (ASSL) | Microsoft Docs
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
apiname: IncrementalProcessingNotification Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: IncrementalProcessingNotification element
ms.assetid: bfc9b0a4-4043-4aaf-82d9-67e7f1d1eb81
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1a766604a7fd9866ff790f03024f7047e23138c4
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="incrementalprocessingnotification-element-assl"></a>Elemento IncrementalProcessingNotification (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém informações para o [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) elemento sobre uma consulta a ser executada para determinar o andamento do processamento incremental.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<IncrementalProcessingNotifications>  
   <IncrementalProcessingNotification xsi:type="IncrementalProcessingNotification">...</IncrementalProcessingNotification>  
</IncrementalProcessingNotifications>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[IncrementalProcessingNotification](../../../analysis-services/scripting/data-type/incrementalprocessingnotification-data-type-assl.md)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-n: elemento obrigatório que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[IncrementalProcessingNotifications](../../../analysis-services/scripting/collections/incrementalprocessingnotifications-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.IncrementalProcessingNotification>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de dados ProactiveCachingQueryBinding &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/proactivecachingquerybinding-data-type-assl.md)   
 [Elemento ProactiveCaching &#40; ASSL &#41;](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)   
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
