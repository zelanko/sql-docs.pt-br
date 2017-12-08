---
title: Elemento EstimatedPerformanceGain (ASSL) | Microsoft Docs
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
apiname: EstimatedPerformanceGain Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: EstimatedPerformanceGain
helpviewer_keywords: EstimatedPerformanceGain element
ms.assetid: d7487977-73c3-4244-ad5d-3c357b219db4
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b574ee4d98186ad406e7f3a763bc07ee5d5a7abd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="estimatedperformancegain-element-assl"></a>Elemento EstimatedPerformanceGain (ASSL)
  Contém a porcentagem somente leitura de ganho de desempenho estimado para a partição.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AggregationDesign>  
      ...  
   <EstimatedPerformanceGain>...</EstimatedPerformanceGain>  
   ...  
</AggregationDesign>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Integer|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente para o pai do **EstimatedPerformanceGain** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.AggregationDesign>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
