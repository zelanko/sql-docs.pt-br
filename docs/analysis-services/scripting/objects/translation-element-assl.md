---
title: Elemento Translation (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Translation Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Translation
helpviewer_keywords:
- Translation element
ms.assetid: fe715bab-050d-49e6-8ba6-801d0fa379a4
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8f6dd8a6620cc87f50eeb8be7fe17963fa8548b1
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="translation-element-assl"></a>Elemento Translation (ASSL)
  Fornece uma tradução localizada para o pai da coleção [Translations](../../../analysis-services/scripting/collections/translations-element-assl.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Translations>  
   <Translation xsi:type="Translation">...</Translation>  
   <!-- or -->  
   <Translation xsi:type="AttributeTranslation">...</Translation>  
</Translations>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[Translation](../../../analysis-services/scripting/data-type/translation-data-type-assl.md), [AttributeTranslation](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Traduções](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Translation>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

