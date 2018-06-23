---
title: Tipo de dados MeasureGroupBinding (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MeasureGroupBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MeasureGroupBinding
helpviewer_keywords:
- MeasureGroupBinding data type
ms.assetid: 47e83eec-e0bc-4118-9a0f-5bfdd6218297
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 12c54f8a61d75afd7689f19b2936bb6aefa3b4c1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122489"
---
# <a name="measuregroupbinding-data-type-assl"></a>Tipo de dados MeasureGroupBinding (ASSL)
  Define um tipo de dados derivado que representa uma associação a um [MeasureGroup](../objects/group-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MeasureGroupBinding>  
   <!-- The following elements extend Binding -->  
   <DataSourceID>...</DataSourceID>  
   <CubeID>...</CubeID>  
   <MeasureGroupID>...</MeasureGroupID>  
   <Persistence>...</Persistence>  
   <RefreshPolicy>...</RefreshPolicy>  
   <RefreshInterval>...</RefreshInterval>  
   <Filter>...</Filter>  
</MeasureGroupBinding>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|[Associação](binding-data-type-assl.md)|  
|Tipos de dados derivados|Nenhum|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhum|  
|Elementos filho|[CubeID](../properties/id-element-assl.md), [DataSourceID](../properties/datasourceid-element-assl.md), [filtro](../properties/filter-element-binding-assl.md), [MeasureGroupID](../properties/measuregroupid-element-assl.md), [persistência](../properties/persistence-element-assl.md), [RefreshInterval ](../properties/refreshinterval-element-assl.md), [RefreshPolicy](../properties/refreshpolicy-element-assl.md)|  
|Elementos derivados|Consulte [de associação](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Para obter informações adicionais sobre o `Binding` tipo, incluindo as tabelas de objetos do Analysis Services Scripting Language (ASSL) do tipo de associação e a hierarquia de herança de `Binding` tipos, consulte [tipo de dados de associação &#40;ASSL &#41;](binding-data-type-assl.md).  
  
 Para obter uma visão geral de associações de dados em ASSL, consulte [fontes de dados e associações &#40;multidimensionais do SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.MeasureGroupBinding>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  