---
title: Elemento UnknownMemberTranslation (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- UnknownMemberTranslation Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- UnknownMemberTranslation
helpviewer_keywords:
- UnknownElementTranslation element
ms.assetid: a4b8cdac-b065-4a44-b251-c5ac1cfe5e6f
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 7631f5f214203271dd92472bdd99c628a33f61b7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="unknownmembertranslation-element-assl"></a>Elemento UnknownMemberTranslation (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
## <a name="remarks"></a>Remarks  
 O elemento que corresponde ao pai do **UnknownMemberTranslation** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Translation &#40;ASSL&#41;](../../../analysis-services/scripting/objects/translation-element-assl.md)   
 [Objetos de & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
