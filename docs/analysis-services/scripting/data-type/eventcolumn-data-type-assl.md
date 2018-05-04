---
title: Tipo de dados EventColumn (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- EventColumn Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- EventColumn
helpviewer_keywords:
- EventColumn data type
ms.assetid: c0009f1d-d136-4155-9a1b-7baacda4b552
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b21fbd7ca3d87398e9a7fef22aa51a8955978434
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="eventcolumn-data-type-assl"></a>Tipo de dados EventColumn (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define um tipo de dados primitivos que representa uma coluna de informações a serem capturadas para um elemento [Event](../../../analysis-services/scripting/objects/event-element-assl.md) como parte de um elemento [Trace](../../../analysis-services/scripting/objects/trace-element-assl.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<EventColumn>  
   <ColumnID>...</ColumnID>  
</EventColumn>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|Nenhuma|  
|Tipos de dados derivados|Nenhuma|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|[ColumnID](../../../analysis-services/scripting/properties/columnid-element-eventcolumn-assl.md)|  
|Elementos derivados|[Coluna](../../../analysis-services/scripting/objects/column-element-assl.md) ([colunas](../../../analysis-services/scripting/collections/columns-element-assl.md) coleção de [rastreamento](../../../analysis-services/scripting/objects/trace-element-assl.md))|  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Events &#40;ASSL&#41;](../../../analysis-services/scripting/collections/events-element-assl.md)   
 [Tipos de dados XML de linguagem de script & #40; do Analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
