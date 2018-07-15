---
title: Elemento UnknownMemberTranslation (ASSL) | Microsoft Docs
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
- UnknownMemberTranslation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- UnknownMemberTranslation
helpviewer_keywords:
- UnknownElementTranslation element
ms.assetid: a4b8cdac-b065-4a44-b251-c5ac1cfe5e6f
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 68270cff61daace55131454b549f12880f3b5e6b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37220296"
---
# <a name="unknownmembertranslation-element-assl"></a>Elemento UnknownMemberTranslation (ASSL)
  Contém uma tradução para a legenda do [UnknownMember](member-element-assl.md) elemento para um [dimensão](dimension-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<UnknownMemberTranslations>  
   <UnknownMemberTranslation xsi:type="Translation">...</UnknownMemberTranslation>  
</UnknownMemberTranslations>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[Tradução](../data-type/translation-data-type-assl.md)|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[UnknownMemberTranslations](../collections/translations-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O elemento que corresponde ao pai de `UnknownMemberTranslation` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Translation &#40;ASSL&#41;](translation-element-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
