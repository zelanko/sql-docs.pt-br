---
title: Elemento Events (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
apiname: Events Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Events
helpviewer_keywords: Events element
ms.assetid: de887998-dc4b-44dc-8fec-08d67b92f96d
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7fb5421596d38a01418efccfa1fdfbe97ed2c9b4
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="events-element-assl"></a>Elemento Events (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Define a coleção de [evento](../../../analysis-services/scripting/objects/event-element-assl.md) elementos a serem capturados por um [rastreamento](../../../analysis-services/scripting/objects/trace-element-assl.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Trace>  
   ...  
   <Events>  
      <Event>...</Event>  
   </Events>  
   ...  
</Trace>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Rastreamento](../../../analysis-services/scripting/objects/trace-element-assl.md)|  
|Elementos filho|[Evento](../../../analysis-services/scripting/objects/event-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.TraceEventCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de rastreamentos &#40; ASSL &#41;](../../../analysis-services/scripting/collections/traces-element-assl.md)   
 [Coleções de &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
