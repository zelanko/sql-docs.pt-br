---
title: Elemento ColumnID (EventColumn) (ASSL) | Microsoft Docs
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
- ColumnID Element (EventColumn)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ColumnID
helpviewer_keywords:
- ColumnID element
ms.assetid: c4f4fbad-9d70-4de2-8cf7-caee80a4a1e4
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 71e51ec736b10a6d72621efb2a9b094882ed8057
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121788"
---
# <a name="columnid-element-eventcolumn-assl"></a>Elemento ColumnID (EventColumn) (ASSL)
  Contém o identificador (ID) da coluna de informações a serem capturadas para um evento como parte de um [rastreamento](../objects/trace-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<EventColumn>  
   <ColumnID>...</ColumnID>  
</EventColumn>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-1: elemento obrigatório que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[EventColumn](../data-type/eventcolumn-data-type-assl.md)|  
|Elementos filho|Nenhum.|  
  
## <a name="remarks"></a>Remarks  
 O elemento que corresponde ao pai do `ColumnID` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.TraceColumn>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Columns &#40;ASSL&#41;](../collections/columns-element-assl.md)   
 [Elemento Event &#40;ASSL&#41;](../objects/event-element-assl.md)   
 [Elemento Events &#40;ASSL&#41;](../collections/events-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  