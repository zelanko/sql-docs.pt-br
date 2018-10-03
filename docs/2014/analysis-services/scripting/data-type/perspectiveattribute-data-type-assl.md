---
title: Tipo de dados PerspectiveAttribute (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- PerspectiveAttribute Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- PerspectiveAttribute
helpviewer_keywords:
- PerspectiveAttribute data type
ms.assetid: bf4d45c1-e48d-4ada-bbab-49c3ac74948d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3d5e6220f4767d7cfb4b49553625426b5a499817
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48055176"
---
# <a name="perspectiveattribute-data-type-assl"></a>Tipo de dados PerspectiveAttribute (ASSL)
  Define um tipo de dados primitivo que representa informações sobre um atributo em uma [PerspectiveDimension](dimension-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<PerspectiveAttribute>  
      <AttributeID>...</AttributeID>  
   <DefaultMember>...</DefaultMember>  
   <AttributeHierarchyVisible>...</AttributeHierarchyVisible>  
      <Annotations>...</Annotations>  
</PerspectiveAttribute>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|None|  
|Tipos de dados derivados|None|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|None|  
|Elementos filho|[Anotações](../collections/annotations-element-assl.md), [AttributeHierarchyVisible](../properties/visible-element-assl.md), [AttributeID](../properties/id-element-assl.md), [DefaultMember](../objects/member-element-assl.md)|  
|Elementos derivados|[Atributo](../objects/attribute-element-assl.md) ([atributos](../collections/attributes-element-assl.md) coleção de [PerspectiveDimension](dimension-data-type-assl.md))|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.PerspectiveAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
