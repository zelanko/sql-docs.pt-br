---
title: Tipo de dados Hierarchy (ASSL) | Microsoft Docs
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
- Hierarchy Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Hierarchy data type
ms.assetid: 2e05917e-7e5d-4dd1-817b-4ff5647747ff
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 14354458e3441c6f8f2691350e9236f2aecb6cdd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122738"
---
# <a name="hierarchy-data-type-assl"></a>Tipo de dados Hierarchy (ASSL)
  Define um tipo de dados primitivo que representa uma hierarquia em uma dimensão.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Hierarchy>  
   <Name>...</Name>  
   <ID>...</ID>  
   <Description>...</Description>  
   <DisplayFolder>...</DisplayFolder>  
   <Translations>...</Translations>  
   <AllMemberName>...</AllMemberName>  
   <AllMemberTranslations>...</AllMemberTranslation>  
   <MemberNamesUnique>...</MemberNamesUnique>  
   <AllowDuplicateNames>...</AllowDuplicateNames>  
   <Levels>...</Levels>  
   <Annotations>...</Annotation>  
</Hierarchy>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|Nenhum|  
|Tipos de dados derivados|Nenhum|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhum|  
|Elementos filho|[AllMemberName](../properties/name-element-assl.md), [AllMemberTranslations](../collections/translations-element-assl.md), [AllowDuplicateNames](../properties/allowduplicatenames-element-assl.md), [Annotations](../collections/annotations-element-assl.md), [Description](../properties/description-element-assl.md), [DisplayFolder](../properties/displayfolder-element-assl.md), [ID](../properties/id-element-assl.md), [Levels](../collections/levels-element-assl.md), [MemberNamesUnique](../properties/membernamesunique-element-assl.md), [Name](../properties/name-element-assl.md), [Translations](../collections/translations-element-assl.md)|  
|Elementos derivados|[Hierarchy](../objects/hierarchy-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento *MemberNamesUnique* não tem suporte no DevelopmentMode 1 ou 2 para modos de servidor SharePoint ou Tabular, respectivamente.  
  
 O elemento *MemberKeysUnique* não tem suporte no DevelopmentMode 1 ou 2 para modos de servidor SharePoint ou Tabular, respectivamente.  
  
 O elemento *AllowDuplicateNames* não tem suporte no DevelopmentMode 1 ou 2 para modos de servidor SharePoint ou Tabular, respectivamente.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Hierarchy>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  