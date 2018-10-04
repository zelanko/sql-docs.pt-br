---
title: Tempo de elemento (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Time Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.time
- urn:schemas-microsoft-com:xml-analysis#Time
- http://schemas.microsoft.com/analysisservices/2003/engine#Time
helpviewer_keywords:
- Time element
ms.assetid: b74ba333-19e5-407d-92ab-3c429d4b3f45
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6fae6c91e8659eeef91d02762729011936e60145
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48100097"
---
# <a name="time-element-xmla"></a>Elemento Time (XMLA)
  Especifica o limite de tempo usado pelo comando [DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md) para projetar agregações.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DesignAggregations>  
   ...  
   <Time>...</Time>  
   ...  
</DesignAggregations>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Duração|  
|Valor padrão|None|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
