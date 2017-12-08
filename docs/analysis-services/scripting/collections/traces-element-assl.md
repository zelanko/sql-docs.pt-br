---
title: Rastreia o elemento (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
apiname: Traces Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Traces
helpviewer_keywords: Traces element
ms.assetid: 7ca2c7d1-fda3-4c76-9e32-fd9b5dda56e9
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: afa73f44f7a72579a4c8476ff0053dce828435a1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="traces-element-assl"></a>Elemento Traces (ASSL)
  Contém a coleção de elementos [Trace](../../../analysis-services/scripting/objects/trace-element-assl.md) associados a um elemento [Server](../../../analysis-services/scripting/objects/server-element-assl.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Server>  
      ...  
   <Traces>  
      <Trace>...</Trace>  
   </Traces>  
   ...  
</Server>  
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
|Elementos pai|[Servidor](../../../analysis-services/scripting/objects/server-element-assl.md)|  
|Elementos filho|[Rastreamento](../../../analysis-services/scripting/objects/trace-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.TraceCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Coleções de &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
