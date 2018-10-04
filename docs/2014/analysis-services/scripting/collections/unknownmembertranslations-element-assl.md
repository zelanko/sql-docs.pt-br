---
title: Elemento UnknownMemberTranslations (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- UnknownMemberTranslations Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- UnknownMemberTranslations
helpviewer_keywords:
- UnknownMemberTranslations element
ms.assetid: 72920843-2d43-4ff4-b38e-19c9a7451cb2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 24f9aa5470bc1283abc0fd2b50838dca880ed6d4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48113537"
---
# <a name="unknownmembertranslations-element-assl"></a>Elemento UnknownMemberTranslations (ASSL)
  Contém a coleção de traduções para a legenda do [UnknownMember](../objects/member-element-assl.md) elemento de uma dimensão.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Dimension>  
   ...  
   <UnknownMemberTranslations>  
      <UnknownMemberTranslation xsi:type="Translation ">...</UnknownMemberTranslation>  
      </UnknownMemberTranslations>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|None|  
|Valor padrão|None|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Dimension](../objects/dimension-element-assl.md)|  
|Elementos filho|[UnknownMemberTranslation](../objects/translation-element-assl.md) do tipo [tradução](../data-type/translation-data-type-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento que corresponde ao pai de `UnknownMemberTranslations` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de dados Translation &#40;ASSL&#41;](../data-type/translation-data-type-assl.md)   
 [Coleções &#40;ASSL&#41;](collections-assl.md)  
  
  
