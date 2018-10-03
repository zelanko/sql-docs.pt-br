---
title: Elemento NamingTemplateTranslation (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- NamingTemplateTranslation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- NamingTemplateTranslation
helpviewer_keywords:
- NamingTemplateTranslation element
ms.assetid: 4a97a31d-23bc-4afd-a4dc-bc0ad7121f08
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7689c1b2d83abb7673253550e133cd0fa0ea5e20
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48086247"
---
# <a name="namingtemplatetranslation-element-assl"></a>Elemento NamingTemplateTranslation (ASSL)
  Fornece uma tradução localizada do [NamingTemplate](../properties/namingtemplate-element-assl.md) elemento para um pai [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md) tipo de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<NamingTemplateTranslations>  
   <NamingTemplateTranslation xsi:type="Translation">...</NamingTemplateTranslation>  
</NamingTemplateTranslations>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[Tradução](translation-element-assl.md)|  
|Valor padrão|None|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[NamingTemplateTranslations](../collections/translations-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O valor da `NamingTemplateTranslation` elemento é usado somente por atributos pai (em outras palavras, o valor da [uso](../properties/usage-element-dimensionattribute-assl.md) elemento do `DimensionAttribute` pai está definido como *pai*) para armazenar o localizada tradução do `NamingTemplate` valor para um determinado idioma.  
  
 O elemento que corresponde ao pai de `NamingTemplateTranslations` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento NamingTemplate &#40;ASSL&#41;](../properties/namingtemplate-element-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
