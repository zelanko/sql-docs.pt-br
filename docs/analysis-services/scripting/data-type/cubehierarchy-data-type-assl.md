---
title: Tipo de dados CubeHierarchy (ASSL) | Microsoft Docs
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
- CubeHierarchy Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- CubeHierarchy
helpviewer_keywords:
- CubeHierarchy data type
ms.assetid: cd633409-0c14-4dd9-97cc-3d30e25df24f
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f25f0c95313912a5cfd3f0ce197eb3e40483aebb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="cubehierarchy-data-type-assl"></a>Tipo de dados CubeHierarchy (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define um tipo de dados primitivo que representa informações sobre um [hierarquia](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) elemento em um [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<CubeHierarchy>   <HierarchyID>...</HierarchyID>   <Name>...</Name>   <OptimizedState>...</OptimizedState>   <Visible>...</Visible>   <Enabled>...</Enabled>   <Annotations>...</Annotations></CubeHierarchy>  
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
|Elementos filho|[Anotações](../../../analysis-services/scripting/collections/annotations-element-assl.md), [habilitado](../../../analysis-services/scripting/properties/enabled-element-assl.md), [HierarchyID](../../../analysis-services/scripting/properties/hierarchyid-element-assl.md), [nome](../../../analysis-services/scripting/properties/name-element-assl.md), [OptimizedState](../../../analysis-services/scripting/properties/optimizedstate-element-assl.md), [visíveis](../../../analysis-services/scripting/properties/visible-element-assl.md)|  
|Elementos derivados|[Hierarquia](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) ([hierarquias](../../../analysis-services/scripting/collections/hierarchies-element-assl.md) coleção de [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 Este tipo de dados não tem nenhuma restrição e pode ser usado em nenhum modo de implantação: 0-Multidimensional e Mineração de Dados, 1-SharePoint, e 2-Tabular.  
  
 No SQL Server 2016 Analysis Services e posterior, o *habilitado* propriedade não pode ser definida como **False** para *CubeHierarchy*.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.CubeHierarchy>.  
  
## <a name="see-also"></a>Consulte também  
 [Método Discover &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-methods-discover.md)   
 [Tipos de dados XML de linguagem de script & #40; do Analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
