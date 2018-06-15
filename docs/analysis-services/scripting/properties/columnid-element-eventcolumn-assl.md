---
title: Elemento ColumnID (EventColumn) (ASSL) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e60f8ada3852bdbd09c8f7831b4af0110bb6a630
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34031067"
---
# <a name="columnid-element-eventcolumn-assl"></a>Elemento ColumnID (EventColumn) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contém o identificador (ID) da coluna de informações a serem capturadas para um evento como parte de um [rastreamento](../../../analysis-services/scripting/objects/trace-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<EventColumn>  
   <ColumnID>...</ColumnID>  
</EventColumn>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[EventColumn](../../../analysis-services/scripting/data-type/eventcolumn-data-type-assl.md)|  
|Elementos filho|Nenhuma.|  
  
## <a name="remarks"></a>Remarks  
 O elemento que corresponde ao pai do **ColumnID** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.TraceColumn>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Columns &#40;ASSL&#41;](../../../analysis-services/scripting/collections/columns-element-assl.md)   
 [Elemento Event &#40;ASSL&#41;](../../../analysis-services/scripting/objects/event-element-assl.md)   
 [Elemento Events &#40;ASSL&#41;](../../../analysis-services/scripting/collections/events-element-assl.md)   
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
