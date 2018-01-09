---
title: Elemento hierarchies (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Hierarchies Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Hierarchies
helpviewer_keywords: Hierarchies element
ms.assetid: dc844eea-869c-4217-b9be-e543a76f5e92
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6ef6b15dfe25df203421c807806923947d121ff2
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="hierarchies-element-assl"></a>Elemento Hierarchies (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém a coleção de [hierarquia](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) elementos associados ao elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Dimension> <!-- or CubeDimension, PerspectiveDimension -->  
   ...  
   <Hierarchies>  
            <Hierarchy>...</Hierarchy> <!-- parent: Dimension -->  
      <!-- or -->  
      <Hierarchy xsi:type="CubeHierarchy">...</Hierarchy> <!-- parent: CubeDimension -->  
     <!-- or -->  
      <Hierarchy xsi:type="PerspectiveHierarchy">...</Hierarchy> <!-- parent: PerspectiveDimension -->  
   <Hierarchies>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md), [dimensão](../../../analysis-services/scripting/objects/dimension-element-assl.md), [PerspectiveDimension](../../../analysis-services/scripting/data-type/perspectivedimension-data-type-assl.md)|  
|Elementos filho|Consulte a tabela a seguir.|  
  
|Ancestral ou pai|Elemento filho|  
|------------------------|-------------------|  
|[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)|[Hierarquia](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) do tipo [CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md)|  
|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|[Hierarchy](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)|  
|[PerspectiveDimension](../../../analysis-services/scripting/data-type/perspectivedimension-data-type-assl.md)|[Hierarquia](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) do tipo [PerspectiveHierarchy](../../../analysis-services/scripting/data-type/perspectivehierarchy-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Os elementos correspondentes no modelo de objeto AMO (Objetos de Gerenciamento de Análise) são <xref:Microsoft.AnalysisServices.HierarchyCollection>, <xref:Microsoft.AnalysisServices.CubeHierarchyCollection> e <xref:Microsoft.AnalysisServices.PerspectiveHierarchyCollection>.  
  
## <a name="see-also"></a>Consulte Também  
 [Coleções de &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
