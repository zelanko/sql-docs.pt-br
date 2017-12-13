---
title: Tipo de dados PerspectiveMeasureGroup (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
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
apiname: PerspectiveMeasureGroup Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: PerspectiveMeasureGroup
helpviewer_keywords: PerspectiveMeasureGroup data type
ms.assetid: 5927120d-f30e-4f87-8523-6d17012817d7
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b61e7cc3761f7dfa0783caf34a399d81b6955c8f
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="perspectivemeasuregroup-data-type-assl"></a>Tipo de dados PerspectiveMeasureGroup (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Define um tipo de dados primitivo que representa informações sobre um grupo de medidas em um [perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<PerspectiveMeasureGroup>  
   <MeasureGroupID>...</MeasureGroupID>  
   <Measures>...</Measures>  
   <Annotations>...</Annotations>  
</PerspectiveMeasureGroup>  
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
|Elementos filho|[Anotações](../../../analysis-services/scripting/collections/annotations-element-assl.md), [MeasureGroupID](../../../analysis-services/scripting/properties/measuregroupid-element-assl.md), [medidas](../../../analysis-services/scripting/collections/measures-element-assl.md)|  
|Elementos derivados|[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md) ([MeasureGroups](../../../analysis-services/scripting/collections/measuregroups-element-assl.md) coleção de [perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>Comentários  
 Um grupo de medidas em uma perspectiva tem a mesma estrutura que um grupo de medidas no cubo subjacente.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.PerspectiveMeasureGroup>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script &#40; do Analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
