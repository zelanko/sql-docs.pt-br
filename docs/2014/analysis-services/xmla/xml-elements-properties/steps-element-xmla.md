---
title: As etapas de elemento (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Steps Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Steps
- microsoft.xml.analysis.steps
- urn:schemas-microsoft-com:xml-analysis#Steps
helpviewer_keywords:
- Steps element
ms.assetid: a6821a2a-89ec-418b-b2dd-92adf2ccc20e
caps.latest.revision: 10
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: cfafdc9aa9644b028d66b844550175a462a0258a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122012"
---
# <a name="steps-element-xmla"></a>Elemento Steps (XMLA)
  Especifica o número de máximo de etapas usadas pelo comando [DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md) para projetar agregações.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DesignAggregations>  
   ...  
   <Steps>...</Steps>  
   ...  
</DesignAggregations>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Integer|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  