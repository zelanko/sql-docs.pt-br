---
title: Elemento NamingTemplateTranslations (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7688582f8bc68ee4f81b6e9790c5a18764a66f41
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="namingtemplatetranslations-element-assl"></a>Elemento NamingTemplateTranslations (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Fornece uma coleção de traduções localizadas para o elemento [NamingTemplate](../../../analysis-services/scripting/properties/namingtemplate-element-assl.md) do pai [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Attribute xsi:type="DimensionAttribute">  
   ...  
   <NamingTemplateTranslations>  
            <NamingTemplateTranslation xsi:type="Translation">...</NamingTemplateTranslation>  
...</NamingTemplateTranslations>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Attribute](../../../analysis-services/scripting/objects/attribute-element-assl.md) do tipo [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Elementos filho|[NamingTemplateTranslation](../../../analysis-services/scripting/objects/namingtemplatetranslation-element-assl.md) to tipo [Translation](../../../analysis-services/scripting/objects/translation-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 O valor do elemento **NamingTemplateTranslation** é usado somente pelos atributos pai (em outras palavras, o valor do elemento [Usage](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md) do pai **DimensionAttribute** é definido como *Parent*).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Coleções de & #40; ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
