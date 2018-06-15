---
title: Tipo de dados CubeDimensionBinding (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 72bb7c331c3201270acdc2eb2f5892c02843acb1
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34029647"
---
# <a name="cubedimensionbinding-data-type-assl"></a>Tipo de dados CubeDimensionBinding (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define um tipo de dados derivado que representa a associação de um [dimensão](../../../analysis-services/scripting/objects/dimension-element-assl.md), [medidas](../../../analysis-services/scripting/objects/measure-element-assl.md), ou [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) elemento para uma dimensão de cubo.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CubeDimensionBinding>  
      <!-- The following elements extend Binding -->  
   <DataSourceID>...</DataSourceID>  
   <CubeID>...</CubeID>  
   <CubeDimensionID>...</CubeDimensionID>  
   <Filter>...</Filter>  
</CubeDimensionBinding>  
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
|Elementos filho|[CubeDimensionID](../../../analysis-services/scripting/properties/cubedimensionid-element-assl.md), [CubeID](../../../analysis-services/scripting/properties/cubeid-element-assl.md), [DataSourceID](../../../analysis-services/scripting/properties/datasourceid-element-assl.md), [filtro](../../../analysis-services/scripting/properties/filter-element-trace-assl.md)|  
|Elementos derivados|Consulte [Binding](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Para obter informações adicionais sobre o **associação** tipo, incluindo tabelas de objetos do Analysis Services Scripting Language (ASSL) da **associação** tipo e a hierarquia de herança de  **Associação** tipos, consulte [tipo de dados de associação &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 Para obter uma visão geral de associações de dados em ASSL, consulte [fontes de dados e associações & #40; SSAS Multidimensional & #41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.CubeDimensionBinding>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script & #40; do Analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
