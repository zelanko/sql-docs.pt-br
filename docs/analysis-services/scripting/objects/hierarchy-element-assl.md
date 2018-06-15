---
title: Elemento Hierarchy (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 29f3eba8ee5d85164e306a78bbbeafbbf9011912
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34031039"
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
  
  
