---
title: Tipo de dados PerspectiveMeasureGroup (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 093ed311fb1abadb1fe7cc6378e0687996fa03da
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="perspectivemeasuregroup-data-type-assl"></a>Tipo de dados PerspectiveMeasureGroup (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define um tipo de dados primitivo que representa as informações sobre um grupo de medidas em um elemento [Perspective](../../../analysis-services/scripting/objects/perspective-element-assl.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<PerspectiveMeasureGroup>  
   <MeasureGroupID>...</MeasureGroupID>  
   <Measures>...</Measures>  
   <Annotations>...</Annotations>  
</PerspectiveMeasureGroup>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|Nenhuma|  
|Tipos de dados derivados|Nenhuma|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|[Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md), [MeasureGroupID](../../../analysis-services/scripting/properties/measuregroupid-element-assl.md), [Measures](../../../analysis-services/scripting/collections/measures-element-assl.md)|  
|Elementos derivados|[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md) (coleção[MeasureGroups](../../../analysis-services/scripting/collections/measuregroups-element-assl.md) de [Perspective](../../../analysis-services/scripting/objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>Comentários  
 Um grupo de medidas em uma perspectiva tem a mesma estrutura que um grupo de medidas no cubo subjacente.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.PerspectiveMeasureGroup>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script & #40; do Analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
