---
title: Tipo de dados CubeHierarchy (ASSL) | Microsoft Docs
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
- CubeHierarchy Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeHierarchy
helpviewer_keywords:
- CubeHierarchy data type
ms.assetid: cd633409-0c14-4dd9-97cc-3d30e25df24f
caps.latest.revision: 44
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0d719b6c841b27df473599514dc12c4e90644610
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37176193"
---
# <a name="cubehierarchy-data-type-assl"></a>Tipo de dados CubeHierarchy (ASSL)
  Define um tipo de dados primitivo que representa informações sobre um [hierarquia](../objects/hierarchy-element-assl.md) elemento em um [cubo](../objects/cube-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<CubeHierarchy>   <HierarchyID>...</HierarchyID>   <Name>...</Name>   <OptimizedState>...</OptimizedState>   <Visible>...</Visible>   <Enabled>...</Enabled>   <Annotations>...</Annotations></CubeHierarchy>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|Nenhum|  
|Tipos de dados derivados|Nenhum|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhum|  
|Elementos filho|[Anotações](../collections/annotations-element-assl.md), [habilitados](../properties/enabled-element-assl.md), [HierarchyID](../properties/id-element-assl.md), [nome](../properties/name-element-assl.md), [OptimizedState](../properties/state-element-assl.md), [visíveis](../properties/visible-element-assl.md)|  
|Elementos derivados|[Hierarquia](../objects/hierarchy-element-assl.md) ([hierarquias](../collections/hierarchies-element-assl.md) coleção de [CubeDimension](dimension-data-type-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 Este tipo de dados não tem nenhuma restrição e pode ser usado em nenhum modo de implantação: 0-Multidimensional e Mineração de Dados, 1-SharePoint, e 2-Tabular.  
  
 Na [!INCLUDE[ssASCurrent](../../../includes/ssascurrent-md.md)], o *Enabled* propriedade não pode ser definida como `False` para *CubeHierarchy*.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.CubeHierarchy>.  
  
## <a name="see-also"></a>Consulte também  
 [Descobrir o método &#40;XMLA&#41;](../../xmla/xml-elements-methods-discover.md)   
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
