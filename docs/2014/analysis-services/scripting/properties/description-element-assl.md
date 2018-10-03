---
title: Elemento Description (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Description Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Description
helpviewer_keywords:
- Description element
ms.assetid: 34d67e7c-e79a-429b-8cc3-6ca13b9cf9c3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 19a041d81646361d1f6eefb96604829ec1928032
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126126"
---
# <a name="description-element-assl"></a>Elemento Description (ASSL)
  Contém a descrição do elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Action> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Description>...</Description>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|None|  
|Cardinalidade|0-1: elemento opcional que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Ação](../objects/action-element-assl.md), [agregação](../objects/aggregation-element-assl.md), [AggregationDesign](../objects/aggregationdesign-element-assl.md), [Assembly](../objects/assembly-element-assl.md), [AttributePermission](../objects/attributepermission-element-assl.md), [ CalculationProperty](../objects/calculationproperty-element-assl.md), [CellPermission](../objects/cellpermission-element-assl.md), [cubo](../objects/cube-element-assl.md), [CubeDimensionPermission](../data-type/permission-data-type-assl.md), [banco de dados](../objects/database-element-assl.md) , [Fonte de dados](../objects/datasource-element-assl.md), [DataSourceView](../objects/datasourceview-element-assl.md), [dimensão](../objects/dimension-element-assl.md), [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md), [hierarquia](../objects/hierarchy-element-assl.md), [Kpi](../objects/kpi-element-assl.md), [nível](../objects/level-element-assl.md), [MdxScript](../objects/mdxscript-element-assl.md), [medida](../objects/measure-element-assl.md), [MeasureGroup](../objects/group-element-assl.md), [MiningModel](../objects/miningmodel-element-assl.md), [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md), [MiningStructure](../objects/miningstructure-element-assl.md), [MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md), [ Partição](../objects/partition-element-assl.md), [permissão](../data-type/permission-data-type-assl.md), [perspectiva](../objects/perspective-element-assl.md), [função](../objects/role-element-assl.md), [servidor](../objects/server-element-assl.md), [ Rastreamento](../objects/trace-element-assl.md), [tradução](../objects/translation-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O valor de um elemento `Description` tem as seguintes restrições:  
  
-   O valor não pode conter espaços à esquerda ou direita. Se os espaços à esquerda ou à direita serão incluídos no valor de uma `Description` elemento, esses espaços serão implicitamente removidos pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
-   O valor não pode conter caracteres de controle. Se os caracteres de controle forem incluídos no valor de um elemento `Description`, esses caracteres serão implicitamente removidos pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Nomeie o elemento &#40;ASSL&#41;](name-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
