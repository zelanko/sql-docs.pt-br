---
title: Elemento ColumnID (EventColumn) (ASSL) | Microsoft Docs
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
- ColumnID Element (EventColumn)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ColumnID
helpviewer_keywords:
- ColumnID element
ms.assetid: c4f4fbad-9d70-4de2-8cf7-caee80a4a1e4
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4ee429b5ef2d9f0a8d06c0c13c17c71f03cccf84
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
  
  
