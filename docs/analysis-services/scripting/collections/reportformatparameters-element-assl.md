---
title: Elemento ReportFormatParameters (ASSL) | Microsoft Docs
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
- ReportFormatParameters Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ReportFormatParameters
helpviewer_keywords:
- ReportFormatParameters element
ms.assetid: f2e677bf-7b6b-4ce4-b0ec-75a4999306c9
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 7419263822de734254a43042afdfae8e627a8c4a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="reportformatparameters-element-assl"></a>Elemento ReportFormatParameters (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contém a coleção de elementos [ReportFormatParameter](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md) para um elemento [ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Action xsi:type="ReportAction">  
   ...  
   <ReportFormatParameters>  
      <ReportFormatParameter>...</ReportFormatParameter>  
   </ReportFormatParameters>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Action](../../../analysis-services/scripting/objects/action-element-assl.md) do tipo [ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)|  
|Elementos filho|[ReportFormatParameter](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento que corresponde ao pai do **ReportFormatParameters** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ReportAction>.  
  
## <a name="see-also"></a>Consulte também  
 [Coleções de & #40; ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
