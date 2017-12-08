---
title: Tipo de dados CubeAttributeBinding (ASSL) | Microsoft Docs
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
apiname: CubeAttributeBinding Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: CubeAttributeBinding
helpviewer_keywords: CubeAttributeBinding data type
ms.assetid: 04e3d619-1de8-4fc8-a089-9a44ac0f930c
caps.latest.revision: "41"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4496205dca5947ec164162f68be2d3143b3ff024
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|[Associação](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
|Tipos de dados derivados|Nenhuma|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|[AttributeID](../../../analysis-services/scripting/properties/attributeid-element-assl.md), [CubeDimensionID](../../../analysis-services/scripting/properties/cubedimensionid-element-assl.md), [CubeID](../../../analysis-services/scripting/properties/cubeid-element-assl.md), [Ordinal](../../../analysis-services/scripting/properties/ordinal-element-assl.md), [tipo](../../../analysis-services/scripting/properties/type-element-binding-assl.md)|  
|Elementos derivados|Consulte [de associação](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 Para obter informações adicionais sobre o **associação** tipo, incluindo tabelas de objetos do Analysis Services Scripting Language (ASSL) da **associação** tipo e a hierarquia de herança de  **Associação** tipos, consulte [associação de tipo de dados &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 Para obter uma visão geral de associações de dados em ASSL, consulte [fontes de dados e associações &#40; SSAS Multidimensional &#41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.CubeAttributeBinding>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script &#40; do Analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
