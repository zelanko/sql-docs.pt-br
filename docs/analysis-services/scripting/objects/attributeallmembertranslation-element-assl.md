---
title: Elemento AttributeAllMemberTranslation (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: AttributeAllMemberTranslation Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AttributeAllMemberTranslation
helpviewer_keywords: AttributeAllMemberTranslation element
ms.assetid: 4b0c61dd-6666-4bf4-9b23-c9d8e315c414
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 844e9544d196a55b1afea8f532a706964b48e745
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="attributeallmembertranslation-element-assl"></a>Elemento AttributeAllMemberTranslation (ASSL)
  Contém uma tradução para a legenda do **todos os** membro de um [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AttributeAllMemberTranslations>  
   <AttributeAllMemberTranslation xsi:type="Translation">...</AttributeAllMemberTranslation>  
</AttributeAllMemberTranslations>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[Tradução](../../../analysis-services/scripting/data-type/translation-data-type-assl.md)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[AttributeAllMemberTranslations](../../../analysis-services/scripting/collections/attributeallmembertranslations-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O elemento que corresponde ao pai do **AttributeAllMemberTranslations** coleção no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Translation &#40; ASSL &#41;](../../../analysis-services/scripting/objects/translation-element-assl.md)   
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
