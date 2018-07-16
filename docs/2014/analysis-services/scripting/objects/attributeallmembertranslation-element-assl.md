---
title: Elemento AttributeAllMemberTranslation (ASSL) | Microsoft Docs
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
- AttributeAllMemberTranslation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AttributeAllMemberTranslation
helpviewer_keywords:
- AttributeAllMemberTranslation element
ms.assetid: 4b0c61dd-6666-4bf4-9b23-c9d8e315c414
caps.latest.revision: 30
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0d70f1420c0324cf1f1a2b3bb06fb68394268071
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37314686"
---
# <a name="attributeallmembertranslation-element-assl"></a>Elemento AttributeAllMemberTranslation (ASSL)
  Contém uma tradução para a legenda do `All` membro de uma [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AttributeAllMemberTranslations>  
   <AttributeAllMemberTranslation xsi:type="Translation">...</AttributeAllMemberTranslation>  
</AttributeAllMemberTranslations>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[Tradução](../data-type/translation-data-type-assl.md)|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[AttributeAllMemberTranslations](../collections/translations-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O elemento que corresponde ao pai da coleção `AttributeAllMemberTranslations` no modelo de objeto AMO (Objetos de Gerenciamento de Análise) é <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Translation &#40;ASSL&#41;](translation-element-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
