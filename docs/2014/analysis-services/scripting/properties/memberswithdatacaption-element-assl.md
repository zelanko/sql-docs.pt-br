---
title: Elemento MembersWithDataCaption (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MembersWithDataCaption Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MembersWithDataCaption
helpviewer_keywords:
- MembersWithDataCaption element
ms.assetid: a5d59efd-5d67-485b-a360-67d54a1fe394
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 847a355f2517a5a630096e2617a27bdae396e565
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48103896"
---
# <a name="memberswithdatacaption-element-assl"></a>Elemento MembersWithDataCaption (ASSL)
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|None|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[AttributeTranslation](../data-type/translation-data-type-assl.md), [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O valor da `MembersWithDataCaption` elemento é usado somente por atributos pai (em outras palavras, o valor da [uso](usage-element-dimensionattribute-assl.md) elemento do `DimensionAttribute` elemento pai é definido como *pai*) para determinar o legenda dos membros de dados no atributo pai. Para obter mais informações sobre membros de dados, consulte [Atributos em hierarquias pai-filho](../../multidimensional-models/parent-child-dimension-attributes.md).  
  
 Os elementos que correspondem aos pais de `MembersWithDataCaption` no modelo de objeto Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.AttributeTranslation> e <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento MembersWithData &#40;ASSL&#41;](../objects/data-element-assl.md)   
 [Tipo de dados AttributeTranslation &#40;ASSL&#41;](../data-type/translation-data-type-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
