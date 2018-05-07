---
title: Tipo de dados Hierarchy (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f2bb1775f89fc2b6942cdf184e3222a3d2fd2131
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="hierarchy-data-type-assl"></a>Tipo de dados Hierarchy (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|Nenhuma|  
|Tipos de dados derivados|Nenhuma|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|[AllMemberName](../../../analysis-services/scripting/properties/allmembername-element-assl.md), [AllMemberTranslations](../../../analysis-services/scripting/collections/allmembertranslations-element-assl.md), [AllowDuplicateNames](../../../analysis-services/scripting/properties/allowduplicatenames-element-assl.md), [Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md), [Description](../../../analysis-services/scripting/properties/description-element-assl.md), [DisplayFolder](../../../analysis-services/scripting/properties/displayfolder-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [Levels](../../../analysis-services/scripting/collections/levels-element-assl.md), [MemberNamesUnique](../../../analysis-services/scripting/properties/membernamesunique-element-assl.md), [Name](../../../analysis-services/scripting/properties/name-element-assl.md), [Translations](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
|Elementos derivados|[Hierarquia](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento *MemberNamesUnique* não tem suporte no DevelopmentMode 1 ou 2 para modos de servidor SharePoint ou Tabular, respectivamente.  
  
 O elemento *MemberKeysUnique* não tem suporte no DevelopmentMode 1 ou 2 para modos de servidor SharePoint ou Tabular, respectivamente.  
  
 O elemento *AllowDuplicateNames* não tem suporte no DevelopmentMode 1 ou 2 para modos de servidor SharePoint ou Tabular, respectivamente.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Hierarchy>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script & #40; do Analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
