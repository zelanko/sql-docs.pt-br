---
title: Elemento HierarchyID (ASSL) | Microsoft Docs
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
apiname: HierarchyID Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: HierarchyID
helpviewer_keywords: HierarchyID element
ms.assetid: 6effe47d-e598-41f8-993a-b2bce49fd7dd
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 55069e605d3cb4fa71463e334932cbc048ea5f46
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="hierarchyid-element-assl"></a>Elemento HierarchyID (ASSL)
  Contém o identificador (ID) para um [CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md), [MeasureGroupHierarchy](../../../analysis-services/scripting/data-type/measuregrouphierarchy-data-type-assl.md), ou [PerspectiveHierarchy](../../../analysis-services/scripting/data-type/perspectivehierarchy-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CubeHierarchy> <!-- or MeasureGroupHierarchy, PerspectiveHierarchy -->  
      ...  
   <HierarchyID>...</HierarchyID>  
      ...  
</CubeHierarchy>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md), [MeasureGroupHierarchy](../../../analysis-services/scripting/data-type/measuregrouphierarchy-data-type-assl.md), [PerspectiveHierarchy](../../../analysis-services/scripting/data-type/perspectivehierarchy-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Os elementos que correspondem aos pais de **HierarchyID** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.CubeHierarchy> e <xref:Microsoft.AnalysisServices.PerspectiveHierarchy>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
