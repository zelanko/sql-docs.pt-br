---
title: Elemento NamingTemplateTranslation (ASSL) | Microsoft Docs
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
caps.latest.revision: 29
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a2832ae5ffe9d5b834fc03f84154fa398b7a19fd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37167547"
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
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[NamingTemplateTranslations](../collections/translations-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor da `NamingTemplateTranslation` elemento é usado somente por atributos pai (em outras palavras, o valor da [uso](../properties/usage-element-dimensionattribute-assl.md) elemento do `DimensionAttribute` pai está definido como *pai*) para armazenar o localizada tradução do `NamingTemplate` valor para um determinado idioma.  
  
 O elemento que corresponde ao pai de `NamingTemplateTranslations` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento NamingTemplate &#40;ASSL&#41;](../properties/namingtemplate-element-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
