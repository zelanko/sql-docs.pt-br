---
title: Elemento ReportParameters (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ReportParameters Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ReportParameters
helpviewer_keywords: ReportParameters element
ms.assetid: 0e138e8f-8313-47f2-96e1-cd189eec26bb
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 61b863015757214818a829b1a835e8cbbd41e111
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="reportparameters-element-assl"></a>Elemento ReportParameters (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém a coleção de [ReportParameter](../../../analysis-services/scripting/objects/reportparameter-element-assl.md) elementos para um [ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Action xsi:type="ReportAction">  
   ...  
   <ReportParameters>  
      <ReportParameter>...</ReportParameter>  
   </ReportParameters>  
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
|Elementos filho|[ReportParameter](../../../analysis-services/scripting/objects/reportparameter-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.ReportParameterCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Coleções de &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
