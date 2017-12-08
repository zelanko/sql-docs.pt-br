---
title: Elemento UnknownMemberTranslation (ASSL) | Microsoft Docs
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
apiname: UnknownMemberTranslation Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: UnknownMemberTranslation
helpviewer_keywords: UnknownElementTranslation element
ms.assetid: a4b8cdac-b065-4a44-b251-c5ac1cfe5e6f
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f5e75ab44c48383fcd8b68ddf736c8de60e4478e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="unknownmembertranslation-element-assl"></a>Elemento UnknownMemberTranslation (ASSL)
  Contém uma tradução para a legenda do [UnknownMember](../../../analysis-services/scripting/properties/unknownmember-element-assl.md) elemento para uma [dimensão](../../../analysis-services/scripting/objects/dimension-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<UnknownMemberTranslations>  
   <UnknownMemberTranslation xsi:type="Translation">...</UnknownMemberTranslation>  
</UnknownMemberTranslations>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[Tradução](../../../analysis-services/scripting/data-type/translation-data-type-assl.md)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[UnknownMemberTranslations](../../../analysis-services/scripting/collections/unknownmembertranslations-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O elemento que corresponde ao pai do **UnknownMemberTranslation** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Translation &#40; ASSL &#41;](../../../analysis-services/scripting/objects/translation-element-assl.md)   
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
