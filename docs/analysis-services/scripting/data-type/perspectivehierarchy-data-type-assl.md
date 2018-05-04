---
title: Tipo de dados PerspectiveHierarchy (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- PerspectiveHierarchy Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- PerspectiveHierarchy
helpviewer_keywords:
- PerspectiveHierarchy data type
ms.assetid: 30366bd0-ee1c-4940-8c1f-ca5e0dd5fe4b
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 8853e8c2547941c57e61eb2b5e89517a2348ff44
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="perspectivehierarchy-data-type-assl"></a>Tipo de dados PerspectiveHierarchy (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define um tipo de dados primitivo que representa as informações sobre uma hierarquia em um elemento [PerspectiveDimension](../../../analysis-services/scripting/data-type/perspectivedimension-data-type-assl.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<PerspectiveHierarchy>  
   <HierarchyID>...</HierarchyID>  
      <Annotations>...</Annotations>  
</PerspectiveHierarchy>  
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
|Elementos filho|[Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md), [HierarchyID](../../../analysis-services/scripting/properties/hierarchyid-element-assl.md)|  
|Elementos derivados|[Hierarchy](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) (coleção de[Hierarchies](../../../analysis-services/scripting/collections/hierarchies-element-assl.md) [PerspectiveDimension](../../../analysis-services/scripting/data-type/perspectivedimension-data-type-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.PerspectiveHierarchy>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script & #40; do Analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
