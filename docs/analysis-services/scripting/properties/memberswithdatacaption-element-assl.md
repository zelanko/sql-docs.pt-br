---
title: Elemento MembersWithDataCaption (ASSL) | Microsoft Docs
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
apiname:
- MembersWithDataCaption Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MembersWithDataCaption
helpviewer_keywords:
- MembersWithDataCaption element
ms.assetid: a5d59efd-5d67-485b-a360-67d54a1fe394
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f254c1fb3c747a64e3e8e5df50bf30d532678d09
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

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
  
## <a name="remarks"></a>Comentários  
 O valor da **MembersWithDataCaption** elemento é usado somente por atributos pai (em outras palavras, o valor da [uso](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md) elemento do **DimensionAttribute** pai elemento é definido como *pai*) para determinar a legenda dos membros de dados no atributo pai. Para obter mais informações sobre membros de dados, consulte [Atributos em hierarquias pai-filho](../../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md).  
  
 Os elementos que correspondem aos pais de **MembersWithDataCaption** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.AttributeTranslation> e <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento MembersWithData &#40; ASSL &#41;](../../../analysis-services/scripting/properties/memberswithdata-element-assl.md)   
 [Tipo de dados AttributeTranslation &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

