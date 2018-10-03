---
title: Tipo de dados CubeAttributeBinding (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CubeAttributeBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeAttributeBinding
helpviewer_keywords:
- CubeAttributeBinding data type
ms.assetid: 04e3d619-1de8-4fc8-a089-9a44ac0f930c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6b0bf386c24a27c0c02caec6d71049d6d1eb8d5e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48164016"
---
# <a name="cubeattributebinding-data-type-assl"></a>Tipo de dados CubeAttributeBinding (ASSL)
  Define um tipo de dados derivado que representa a associação de um atributo em uma dimensão de cubo a uma ação ou coluna de estrutura de mineração.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CubeAttributeBinding>  
   <!-- The following elements extend Binding -->  
   <CubeID>...</CubeID>  
   <CubeDimensionID>...</CubeDimensionID>  
      <AttributeID>...</AttributeID>  
      <Type>...</Type>  
   <Ordinal>...</Ordinal>  
</CubeAttributeBinding>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|[Associação](binding-data-type-assl.md)|  
|Tipos de dados derivados|None|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|None|  
|Elementos filho|[AttributeID](../properties/id-element-assl.md), [CubeDimensionID](../properties/dimensionid-element-assl.md), [CubeID](../properties/cubeid-element-assl.md), [Ordinal](../properties/ordinal-element-assl.md), [tipo](../properties/type-element-binding-assl.md)|  
|Elementos derivados|Consulte [de associação](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre o `Binding` tipo, incluindo tabelas de objetos do Analysis Services Scripting Language (ASSL) da `Binding` tipo e a hierarquia de herança dos `Binding` tipos, consulte [ &#40;ASSL&#41;](binding-data-type-assl.md).  
  
 Para uma visão geral de associações de dados em ASSL, consulte [fontes de dados e associações &#40;Multidimensional do SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.CubeAttributeBinding>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
