---
title: O tipo de dados de ação (ASSL) | Microsoft Docs
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 77b4ef3f8507d67090b78c00807278d0d7dc6348
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37154967"
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
|Elementos filho|[Anotações](../collections/annotations-element-assl.md), [aplicativo](../properties/application-element-assl.md), [legenda](../properties/caption-element-assl.md), [CaptionIsMdx](../properties/captionismdx-element-assl.md), [condição](../properties/condition-element-assl.md), [descrição ](../properties/description-element-assl.md), [ID](../properties/id-element-assl.md), [invocação](../properties/invocation-element-assl.md), [nome](../properties/name-element-assl.md), [destino](../properties/target-element-assl.md), [TargetType](../properties/targettype-element-assl.md), [Traduções](../collections/translations-element-assl.md), [tipo](../properties/type-element-action-assl.md)|  
|Elementos derivados|[DrillThroughAction](action-data-type-assl.md), [ReportAction](reportaction-data-type-assl.md), [StandardAction](standardaction-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Para obter mais informações sobre ações, consulte [Ações &#40;Analysis Services – Dados Multidimensionais&#41;](../../multidimensional-models/actions-analysis-services-multidimensional-data.md).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Action>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de cubo &#40;ASSL&#41;](../objects/cube-element-assl.md)   
 [Elemento Perspective &#40;ASSL&#41;](../objects/perspective-element-assl.md)   
 [Tipo de dados PerspectiveAction &#40;ASSL&#41;](perspectiveaction-data-type-assl.md)   
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
