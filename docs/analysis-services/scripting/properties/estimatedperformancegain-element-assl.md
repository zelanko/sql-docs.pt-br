---
title: Elemento EstimatedPerformanceGain (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- EstimatedPerformanceGain Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- EstimatedPerformanceGain
helpviewer_keywords:
- EstimatedPerformanceGain element
ms.assetid: d7487977-73c3-4244-ad5d-3c357b219db4
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c2174ad5e09ffcb78510db337b92b4f372a087f7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="estimatedperformancegain-element-assl"></a>Elemento EstimatedPerformanceGain (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente para o pai do **EstimatedPerformanceGain** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.AggregationDesign>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
