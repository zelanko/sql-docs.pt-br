---
title: Tipo de dados Translation (ASSL) | Microsoft Docs
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
- Translation Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Translation data type
ms.assetid: d40039e1-3ff6-4e20-8d8b-5baf501f726f
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 520ca850d5c1a80ff01ca3e973310c2b2d60e66d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="translation-data-type-assl"></a>Tipo de dados Translation (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define um tipo de dados primitivo que representa uma tradução localizada.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Translation>  
   <Language>...</Language>  
   <Caption>...</Caption>  
   <Description>...</Description>  
   <DisplayFolder>...</DisplayFolder>  
   <Annotations>...</Annotations>  
</Translation>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|Nenhuma|  
|Tipos de dados derivados|[AttributeTranslation](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|[Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md), [Caption](../../../analysis-services/scripting/properties/caption-element-assl.md), [Description](../../../analysis-services/scripting/properties/description-element-assl.md), [DisplayFolder](../../../analysis-services/scripting/properties/displayfolder-element-assl.md), [Language](../../../analysis-services/scripting/properties/language-element-assl.md)|  
|Elementos derivados|[AllMemberTranslation](../../../analysis-services/scripting/objects/allmembertranslation-element-assl.md), [AttributeAllMemberTranslation](../../../analysis-services/scripting/objects/attributeallmembertranslation-element-assl.md), [NamingTemplateTranslation](../../../analysis-services/scripting/objects/namingtemplatetranslation-element-assl.md), [UnknownMemberTranslation](../../../analysis-services/scripting/objects/unknownmembertranslation-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Translation>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script & #40; do Analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
