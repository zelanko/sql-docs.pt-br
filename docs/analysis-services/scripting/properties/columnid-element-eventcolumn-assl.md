---
title: Elemento ColumnID (EventColumn) (ASSL) | Microsoft Docs
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
apiname: ColumnID Element (EventColumn)
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ColumnID
helpviewer_keywords: ColumnID element
ms.assetid: c4f4fbad-9d70-4de2-8cf7-caee80a4a1e4
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c887b78b04f45752a406d618a84078a8e002abba
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="columnid-element-eventcolumn-assl"></a>Elemento ColumnID (EventColumn) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém o identificador (ID) da coluna de informações a serem capturadas para um evento como parte de um [rastreamento](../../../analysis-services/scripting/objects/trace-element-assl.md) elemento.  
  
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
|Elemento pai|[EventColumn](../../../analysis-services/scripting/data-type/eventcolumn-data-type-assl.md)|  
|Elementos filho|Nenhum.|  
  
## <a name="remarks"></a>Remarks  
 O elemento que corresponde ao pai do **ColumnID** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.TraceColumn>.  
  
## <a name="see-also"></a>Consulte Também  
 [Elemento de colunas &#40; ASSL &#41;](../../../analysis-services/scripting/collections/columns-element-assl.md)   
 [Elemento Event &#40; ASSL &#41;](../../../analysis-services/scripting/objects/event-element-assl.md)   
 [Elemento de eventos &#40; ASSL &#41;](../../../analysis-services/scripting/collections/events-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
