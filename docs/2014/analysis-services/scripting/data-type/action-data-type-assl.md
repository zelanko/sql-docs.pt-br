---
title: Tipo de dados de ação (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Action Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Action data type
ms.assetid: 8c4d2ff7-17e1-4e74-bec7-637e0b191acf
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 18047bc8a33c92e6bcd434e1a472917c269272e5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116458"
---
# <a name="action-data-type-assl"></a>Tipo de dados da ação (ASSL)
  Define um tipo de dados primitivo abstrato que representa uma ação em um [cubo](../objects/cube-element-assl.md) elemento ou um [perspectiva](../objects/perspective-element-assl.md) elemento.  
  
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|Nenhum|  
|Tipos de dados derivados|[DrillThroughAction](action-data-type-assl.md), [ReportAction](reportaction-data-type-assl.md), [StandardAction](standardaction-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Ações](../collections/actions-element-assl.md)|  
|Elementos filho|[Annotations](../collections/annotations-element-assl.md), [Application](../properties/application-element-assl.md), [Caption](../properties/caption-element-assl.md), [CaptionIsMdx](../properties/captionismdx-element-assl.md), [Condition](../properties/condition-element-assl.md), [Description](../properties/description-element-assl.md), [ID](../properties/id-element-assl.md), [Invocation](../properties/invocation-element-assl.md), [Name](../properties/name-element-assl.md), [Target](../properties/target-element-assl.md), [TargetType](../properties/targettype-element-assl.md), [Translations](../collections/translations-element-assl.md), [Type](../properties/type-element-action-assl.md)|  
|Elementos derivados|[DrillThroughAction](action-data-type-assl.md), [ReportAction](reportaction-data-type-assl.md), [StandardAction](standardaction-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Para obter mais informações sobre ações, consulte [Ações &#40;Analysis Services – Dados Multidimensionais&#41;](../../multidimensional-models/actions-analysis-services-multidimensional-data.md).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Action>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de cubo &#40;ASSL&#41;](../objects/cube-element-assl.md)   
 [Elemento Perspective &#40;ASSL&#41;](../objects/perspective-element-assl.md)   
 [Tipo de dados PerspectiveAction &#40;ASSL&#41;](perspectiveaction-data-type-assl.md)   
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  