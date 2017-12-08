---
title: "Tipo de dados de ação (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Action Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: Action data type
ms.assetid: 8c4d2ff7-17e1-4e74-bec7-637e0b191acf
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 73003aafb063182adf165cd75b43c2191c818b78
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="action-data-type-assl"></a>Tipo de dados da ação (ASSL)
  Define um tipo de dados primitivo abstrato que representa uma ação em um [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento ou um [perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Action>  
   <Name>...</Name>  
   <ID>...</ID>  
   <Caption>...</Caption>  
      <CaptionIsMdx>...</CaptionIsMdx>  
      <Translations>...</Translations>  
   <TargetType>...</TargetType>  
   <Target>...</Target>  
   <Condition>...</Condition>  
   <Type>...</Type>  
   <Invocation>...</Invocation>  
   <Application>...</Application>  
      <Description>...</Description>  
      <Annotations>...</Annotations>  
</Action>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|Nenhuma|  
|Tipos de dados derivados|[DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md), [ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md), [StandardAction](../../../analysis-services/scripting/data-type/standardaction-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Ações](../../../analysis-services/scripting/collections/actions-element-assl.md)|  
|Elementos filho|[Anotações](../../../analysis-services/scripting/collections/annotations-element-assl.md), [aplicativo](../../../analysis-services/scripting/properties/application-element-assl.md), [legenda](../../../analysis-services/scripting/properties/caption-element-assl.md), [CaptionIsMdx](../../../analysis-services/scripting/properties/captionismdx-element-assl.md), [condição](../../../analysis-services/scripting/properties/condition-element-assl.md), [descrição ](../../../analysis-services/scripting/properties/description-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [invocação](../../../analysis-services/scripting/properties/invocation-element-assl.md), [nome](../../../analysis-services/scripting/properties/name-element-assl.md), [destino](../../../analysis-services/scripting/properties/target-element-assl.md), [TargetType](../../../analysis-services/scripting/properties/targettype-element-assl.md), [Traduções](../../../analysis-services/scripting/collections/translations-element-assl.md), [tipo](../../../analysis-services/scripting/properties/type-element-action-assl.md)|  
|Elementos derivados|[DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md), [ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md), [StandardAction](../../../analysis-services/scripting/data-type/standardaction-data-type-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre ações, consulte [Ações &#40;Analysis Services – Dados Multidimensionais&#41;](../../../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Action>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Cube &#40; ASSL &#41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [Elemento Perspective &#40; ASSL &#41;](../../../analysis-services/scripting/objects/perspective-element-assl.md)   
 [Tipo de dados PerspectiveAction &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/perspectiveaction-data-type-assl.md)   
 [Tipos de dados XML de linguagem de script &#40; do Analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
