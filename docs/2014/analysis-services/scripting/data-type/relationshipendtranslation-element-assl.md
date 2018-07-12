---
title: Elemento RelationshipEndTranslation (ASSL) | Microsoft Docs
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
ms.assetid: 04e09370-fdfe-4051-9998-4a6859ce8c54
caps.latest.revision: 4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 62c779e29ce721289b364599063e1a1de747eb1c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37153017"
---
# <a name="relationshipendtranslation-element-assl"></a>Elemento RelationshipEndTranslation (ASSL)
  Define um tipo de dados primitivo que representa uma tradução localizada para um elemento [RelationshipEnd](relationshipend-data-type-assl.md) .  
  
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|Nenhum|  
|Tipos de dados derivados|[AttributeTranslation](translation-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Traduções](../collections/translations-element-assl.md)|  
|Elementos filho|[Anotações](../collections/annotations-element-assl.md), [Legenda](../properties/caption-element-assl.md), [CollectionCaption](../properties/caption-element-assl.md), [Descrição](../properties/description-element-assl.md), [DisplayFolder](../properties/displayfolder-element-assl.md), [Idioma](../properties/language-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Translation>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
