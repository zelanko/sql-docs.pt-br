---
title: Elemento Goal (ASSL) | Microsoft Docs
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
apiname:
- Goal Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Goal
helpviewer_keywords:
- Goal element
ms.assetid: 75fa5b57-418e-43ad-8704-764e4f0a40cf
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 31a054da277a8ac5df4bc2de468a71b87fffe0f2
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="goal-element-assl"></a>Elemento Goal (ASSL)
  Identifica a meta desejada em uma [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Kpi>  
   ...  
   <Goal>...</Goal>  
   ...  
</Kpi>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[KPI](../../../analysis-services/scripting/objects/kpi-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O elemento **Goal** contém uma linguagem MDX.  
  
 O elemento que corresponde ao pai do **meta** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Kpi>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento status &#40; ASSL &#41;](../../../analysis-services/scripting/properties/status-element-assl.md)   
 [Elemento Trend &#40; ASSL &#41;](../../../analysis-services/scripting/properties/trend-element-assl.md)   
 [Elemento de valor &#40; ASSL &#41;](../../../analysis-services/scripting/properties/value-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

