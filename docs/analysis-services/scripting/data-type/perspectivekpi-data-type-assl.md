---
title: Tipo de dados PerspectiveKpi (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
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
- PerspectiveKpi Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- PerspectiveKpi
helpviewer_keywords:
- PerspectiveKpi data type
ms.assetid: e8d19ec8-70d3-4947-904a-fb81fcac9afd
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a58250d2741a89a5b98451bc37e589f8bce1bd71
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="perspectivekpi-data-type-assl"></a>Tipo de dados PerspectiveKpi (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define um tipo de dados primitivo que representa informações sobre um KPI (indicador chave de desempenho) em um elemento [Perspective](../../../analysis-services/scripting/objects/perspective-element-assl.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<PerspectiveKpi>  
   <KpiID>...</KpiID>  
   <Annotations>...</Annotations>  
</PerspectiveKpi>  
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
|Elementos filho|[Anotações](../../../analysis-services/scripting/collections/annotations-element-assl.md), [KpiID](../../../analysis-services/scripting/properties/kpiid-element-assl.md)|  
|Elementos derivados|[KPI](../../../analysis-services/scripting/objects/kpi-element-assl.md) ([Kpis](../../../analysis-services/scripting/collections/kpis-element-assl.md) coleção de [perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.PerspectiveKpi>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script & #40; do Analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
