---
title: As etapas de elemento (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Steps Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Steps
- microsoft.xml.analysis.steps
- urn:schemas-microsoft-com:xml-analysis#Steps
helpviewer_keywords: Steps element
ms.assetid: a6821a2a-89ec-418b-b2dd-92adf2ccc20e
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 15f64827e38b61007aafb5a76636c2875c6d399c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="steps-element-xmla"></a>Elemento Steps (XMLA)
  Especifica o número de máximo de etapas usadas pelo comando [DesignAggregations](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md) para projetar agregações.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DesignAggregations>  
   ...  
   <Steps>...</Steps>  
   ...  
</DesignAggregations>  
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
|Elementos pai|[DesignAggregations](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
