---
title: Tipo de dados PerspectiveDimension (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: PerspectiveDimension Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: PerspectiveDimension
helpviewer_keywords: PerspectiveDimension data type
ms.assetid: c4bc56de-4f42-4ceb-a68d-a4fec92fdfa9
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: cf9e0b5b26128cea2a6d8f3796db9986550f5300
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="perspectivedimension-data-type-assl"></a>Tipo de dados PerspectiveDimension (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Define um tipo de dados primitivo que representa informações sobre uma dimensão em uma perspectiva.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<PerspectiveDimension>  
   <CubeDimensionID>...</CubeDimensionID>  
   <Attributes>...</Attributes>  
   <Hierarchies>...</Hierarchies>  
      <Annotations>...</Annotations>  
</PerspectiveDimension>  
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
|Elementos filho|[Anotações](../../../analysis-services/scripting/collections/annotations-element-assl.md), [atributos](../../../analysis-services/scripting/collections/attributes-element-assl.md), [CubeDimensionID](../../../analysis-services/scripting/properties/cubedimensionid-element-assl.md), [hierarquias](../../../analysis-services/scripting/collections/hierarchies-element-assl.md)|  
|Elementos derivados|[Dimensão](../../../analysis-services/scripting/objects/dimension-element-assl.md) ([dimensões](../../../analysis-services/scripting/collections/dimensions-element-assl.md) coleção de [perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.PerspectiveDimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script &#40; do Analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
