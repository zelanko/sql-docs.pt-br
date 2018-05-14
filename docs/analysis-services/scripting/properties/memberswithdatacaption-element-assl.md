---
title: Elemento MembersWithDataCaption (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: cc13b853943806854dd4dbc453922f6a4f26dcf7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="memberswithdatacaption-element-assl"></a>Elemento MembersWithDataCaption (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Fornece uma cadeia de caracteres de modelo usada para criar legendas para os membros de dados gerados pelo sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AttributeTranslation> <!-- or DimensionAttribute -->  
   ...  
   <MembersWithDataCaption>...</MembersWithDataCaption>  
   ...  
</AttributeTranslation>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[AttributeTranslation](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md), [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 O valor da **MembersWithDataCaption** elemento é usado somente por atributos pai (em outras palavras, o valor da [uso](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md) elemento do **DimensionAttribute** pai elemento é definido como *pai*) para determinar a legenda dos membros de dados no atributo pai. Para obter mais informações sobre membros de dados, consulte [Atributos em hierarquias pai-filho](../../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md).  
  
 Os elementos que correspondem aos pais de **MembersWithDataCaption** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.AttributeTranslation> e <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento MembersWithData &#40;ASSL&#41;](../../../analysis-services/scripting/properties/memberswithdata-element-assl.md)   
 [Tipo de dados AttributeTranslation &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)   
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
