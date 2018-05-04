---
title: Elemento Hierarchy (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Hierarchy Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Hierarchy
helpviewer_keywords:
- Hierarchy element
ms.assetid: ac54d74a-5e6c-4c24-83bf-766440478f6c
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 47284727e6ed2a3dc757bd11905fd55fbce70d23
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="hierarchy-element-assl"></a>Elemento Hierarchy (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define uma hierarquia em uma dimensão.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Hierarchies>  
   <Hierarchy xsi:type="Hierarchy">...</Hierarchy> <!-- ancestor: Dimension -->  
   <!-- or -->  
   <Hierarchy xsi:type="CubeHierarchy">...</Hierarchy> <!-- ancestor: CubeDimension -->  
   <!-- or -->  
   <Hierarchy xsi:type="PerspectiveHierarchy">...</Hierarchy> <!-- ancestor: PerspectiveDimension -->  
   <!-- or -->  
   <Hierarchy xsi:type="MeasureGroupHierarchy">...</Hierarchy> <!-- ancestor: RegularMeasureGroupDimension -->  
</Hierarchies>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Veja a tabela abaixo.|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
|Ancestral ou pai|Tipo de Dados|  
|------------------------|---------------|  
|[Dimensão](../../../analysis-services/scripting/objects/dimension-element-assl.md)|[Hierarquia](../../../analysis-services/scripting/data-type/hierarchy-data-type-assl.md)|  
|[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)|[CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md)|  
|[PerspectiveDimension](../../../analysis-services/scripting/data-type/perspectivedimension-data-type-assl.md)|[PerspectiveHierarchy](../../../analysis-services/scripting/data-type/perspectivehierarchy-data-type-assl.md)|  
|[RegularMeasureGroupDimension](../../../analysis-services/scripting/data-type/regularmeasuregroupdimension-data-type-assl.md)|[MeasureGroupHierarchy](../../../analysis-services/scripting/data-type/measuregrouphierarchy-data-type-assl.md)|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Hierarquias](../../../analysis-services/scripting/collections/hierarchies-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 Os elementos correspondentes no modelo de objeto AMO (Objetos de Gerenciamento de Análise) são <xref:Microsoft.AnalysisServices.Hierarchy>, <xref:Microsoft.AnalysisServices.CubeHierarchy> e <xref:Microsoft.AnalysisServices.PerspectiveHierarchy>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
