---
title: Elemento UnknownMemberTranslations (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: UnknownMemberTranslations Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: UnknownMemberTranslations
helpviewer_keywords: UnknownMemberTranslations element
ms.assetid: 72920843-2d43-4ff4-b38e-19c9a7451cb2
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f445b85950c05232a5c806a2544cbe02aaf30233
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="unknownmembertranslations-element-assl"></a>Elemento UnknownMemberTranslations (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém a coleção de traduções da legenda do [UnknownMember](../../../analysis-services/scripting/properties/unknownmember-element-assl.md) elemento de uma dimensão.  
  
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
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
|Elementos filho|[UnknownMemberTranslation](../../../analysis-services/scripting/objects/unknownmembertranslation-element-assl.md) do tipo [tradução](../../../analysis-services/scripting/data-type/translation-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento que corresponde ao pai do **UnknownMemberTranslations** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Consulte Também  
 [Tipo de dados Translation &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/translation-data-type-assl.md)   
 [Coleções de &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
