---
title: Elemento SilenceOverrideInterval (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: SilenceOverrideInterval Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: SilenceOverrideInterval
helpviewer_keywords: SilenceOverrideInterval element
ms.assetid: 0dcd2db4-9bc0-4460-b1dd-def0b38c4617
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 807afbc1cabae00efacb04f7389d841e26849e27
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="silenceoverrideinterval-element-assl"></a>Elemento SilenceOverrideInterval (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Define a quantidade de tempo que deve decorrer após o recebimento da notificação inicial antes da geração de imagens MOLAP (OLAP) multidimensionais começa incondicionalmente.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ProactiveCaching>  
   ...  
   <SilenceOverrideInterval>...</SilenceOverrideInterval>  
   ...  
</ProactiveCaching>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|duration|  
|Valor padrão|P0s|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor de **SilenceOverrideInterval** anulará o valor de **SilenceInterval** se uma notificação for recebida durante o período de silêncio.  
  
 O elemento que corresponde ao pai do **SilenceOverrideInterval** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ProactiveCaching>.  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
