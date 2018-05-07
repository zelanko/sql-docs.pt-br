---
title: Elemento UnknownMemberTranslations (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c7a62d2e1306ee2cf434a688dae569a92d3c0eec
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="unknownmembertranslations-element-assl"></a>Elemento UnknownMemberTranslations (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contém a coleção de traduções da legenda do [UnknownMember](../../../analysis-services/scripting/properties/unknownmember-element-assl.md) elemento de uma dimensão.  
  
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Dimensão](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
|Elementos filho|[UnknownMemberTranslation](../../../analysis-services/scripting/objects/unknownmembertranslation-element-assl.md) do tipo [tradução](../../../analysis-services/scripting/data-type/translation-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento que corresponde ao pai do **UnknownMemberTranslations** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de dados Translation &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/translation-data-type-assl.md)   
 [Coleções de & #40; ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
