---
title: Elemento RelationshipEndTranslation (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
applies_to: SQL Server 2016 Preview
ms.assetid: 04e09370-fdfe-4051-9998-4a6859ce8c54
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 715a85f08aef4c4027cf544b9b58da10eb87f850
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="relationshipendtranslation-element-assl"></a>Elemento RelationshipEndTranslation (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Define um tipo de dados primitivo que representa uma tradução localizada para um [RelationshipEnd](../../../analysis-services/scripting/data-type/relationshipend-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<RelationshipEndTranslation>  
   <Language>...</Language>  
   <Caption>...</Caption>  
   <CollectionCaption>...</Caption>  
   <Description>...</Description>  
   <DisplayFolder>...</DisplayFolder>  
   <Annotations>...</Annotations>  
</RelationshipEndTranslation>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|Nenhuma|  
|Tipos de dados derivados|[AttributeTranslation](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Traduções](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
|Elementos filho|[Anotações](../../../analysis-services/scripting/collections/annotations-element-assl.md), [Legenda](../../../analysis-services/scripting/properties/caption-element-assl.md), [CollectionCaption](../../../analysis-services/scripting/properties/caption-element-assl.md), [Descrição](../../../analysis-services/scripting/properties/description-element-assl.md), [DisplayFolder](../../../analysis-services/scripting/properties/displayfolder-element-assl.md), [Idioma](../../../analysis-services/scripting/properties/language-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Translation>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script &#40; do Analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
