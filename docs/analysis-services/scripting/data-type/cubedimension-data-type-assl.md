---
title: Tipo de dados CubeDimension (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e7fd3894b7b1d255a8760da4822eff0de1315b72
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="cubedimension-data-type-assl"></a>Tipo de dados CubeDimension (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define um tipo de dados primitivo que representa a relação entre uma dimensão e um cubo.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CubeDimension>  
      <ID>...</ID>  
   <Name>...</Name>  
   <Translations>...</Translations>  
   <DimensionID>...</DimensionID>  
   <Visible>...</Visible>  
   <AllMemberAggregationUsage>...</AllMemberAggregationUsage>  
   <HierarchyUniqueNameStyle>...</HierarchyUniqueNameStyle>  
   <MemberUniqueNameStyle>...</MemberUniqueNameStyle>  
      <Attributes>...</Attributes>  
   <Hierarchies>...</Hierarchies>  
      <Annotations>...</Annotation>  
</CubeDimension>  
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
|Elementos filho|[AllMemberAggregationUsage](../../../analysis-services/scripting/properties/allmemberaggregationusage-element-assl.md), [Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md), [Attributes](../../../analysis-services/scripting/collections/attributes-element-assl.md), [DimensionID](../../../analysis-services/scripting/properties/dimensionid-element-assl.md), [Hierarchies](../../../analysis-services/scripting/collections/hierarchies-element-assl.md), [HierarchyUniqueNameStyle](../../../analysis-services/scripting/properties/hierarchyuniquenamestyle-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [MemberUniqueNameStyle](../../../analysis-services/scripting/properties/memberuniquenamestyle-element-assl.md), [Name](../../../analysis-services/scripting/properties/name-element-assl.md), [Visible](../../../analysis-services/scripting/properties/visible-element-assl.md), [Translations](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
|Elementos derivados|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md) (coleção[Dimensions](../../../analysis-services/scripting/collections/dimensions-element-assl.md) de [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 Há um elemento **CubeDimension** para cada relação de dimensão em um **Cube**. O elemento **CubeDimension** cobre todos os **MeasureGroups** do cubo.  
  
 Um **CubeDimension** deve incluir um [CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md) se a dimensão tiver algo específico a dizer sobre a hierarquia, incluindo a desabilitação da hierarquia (assim, permitindo a seleção da qual hierarquias aplicam a um uso de dimensão específico), ou fazendo com que a hierarquia invisível.  
  
 Da mesma forma, um **CubeDimension** deve incluir um [CubeAttribute](../../../analysis-services/scripting/data-type/cubeattribute-data-type-assl.md) somente se a dimensão tiver algo específico a dizer sobre o atributo. Não é possível selecionar os atributos aplicáveis a um uso de dimensão específico, visto que os atributos podem ficar invisíveis.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.CubeDimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script & #40; do Analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
