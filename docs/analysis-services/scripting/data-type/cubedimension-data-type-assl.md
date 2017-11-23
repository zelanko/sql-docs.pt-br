---
title: Tipo de dados CubeDimension (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
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
apiname: CubeDimension Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: CubeDimension
helpviewer_keywords: CubeDimension data type
ms.assetid: 128ac790-65a1-4e35-b909-8dba2a61b24c
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 63ce4755b2cf28ec2805b8e0eb32121b399816ab
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="cubedimension-data-type-assl"></a>Tipo de dados CubeDimension (ASSL)
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
|Elementos filho|[AllMemberAggregationUsage](../../../analysis-services/scripting/properties/allmemberaggregationusage-element-assl.md), [anotações](../../../analysis-services/scripting/collections/annotations-element-assl.md), [atributos](../../../analysis-services/scripting/collections/attributes-element-assl.md), [DimensionID](../../../analysis-services/scripting/properties/dimensionid-element-assl.md), [hierarquias](../../../analysis-services/scripting/collections/hierarchies-element-assl.md), [HierarchyUniqueNameStyle](../../../analysis-services/scripting/properties/hierarchyuniquenamestyle-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [MemberUniqueNameStyle](../../../analysis-services/scripting/properties/memberuniquenamestyle-element-assl.md), [nome](../../../analysis-services/scripting/properties/name-element-assl.md), [visível](../../../analysis-services/scripting/properties/visible-element-assl.md), [Traduções](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
|Elementos derivados|[Dimensão](../../../analysis-services/scripting/objects/dimension-element-assl.md) ([dimensões](../../../analysis-services/scripting/collections/dimensions-element-assl.md) coleção de [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md))|  
  
## <a name="remarks"></a>Comentários  
 Há um elemento **CubeDimension** para cada relação de dimensão em um **Cube**. O elemento **CubeDimension** cobre todos os **MeasureGroups** do cubo.  
  
 Um **CubeDimension** deve incluir um [CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md) se a dimensão tiver algo específico a dizer sobre a hierarquia, incluindo a desabilitação da hierarquia (assim, permitindo a seleção da qual hierarquias aplicam a um uso de dimensão específico), ou fazendo com que a hierarquia invisível.  
  
 Da mesma forma, um **CubeDimension** deve incluir um [CubeAttribute](../../../analysis-services/scripting/data-type/cubeattribute-data-type-assl.md) somente se a dimensão tiver algo específico a dizer sobre o atributo. Não é possível selecionar os atributos aplicáveis a um uso de dimensão específico, visto que os atributos podem ficar invisíveis.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.CubeDimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script &#40; do Analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
