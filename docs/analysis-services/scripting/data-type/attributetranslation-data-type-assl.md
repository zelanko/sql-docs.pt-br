---
title: Tipo de dados AttributeTranslation (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: dcc6b3aa016861a7ac2322654886243234cdbf69
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="attributetranslation-data-type-assl"></a>Tipo de dados AttributeTranslation (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define um tipo de dados derivado que representa uma tradução associada a um elemento [Attribute](../../../analysis-services/scripting/objects/attribute-element-assl.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AttributeTranslation>  
   <!-- The following elements extend Translation -->  
   <CaptionColumn>...</CaptionColumn>  
   <MembersWithDataCaption>...</MembersWithDataCaption>  
</AttributeTranslation>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|[Tradução](../../../analysis-services/scripting/data-type/translation-data-type-assl.md)|  
|Tipos de dados derivados|Nenhuma|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|[CaptionColumn](../../../analysis-services/scripting/objects/captioncolumn-element-assl.md), [MembersWithDataCaption](../../../analysis-services/scripting/properties/memberswithdatacaption-element-assl.md)|  
|Elementos derivados|Consulte [Translation](../../../analysis-services/scripting/objects/translation-element-assl.md) (coleção de[Translations](../../../analysis-services/scripting/collections/translations-element-assl.md) [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md) ou [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.AttributeTranslation>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script & #40; do Analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
