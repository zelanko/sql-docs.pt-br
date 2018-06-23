---
title: Tipo de dados CubeDimension (ASSL) | Microsoft Docs
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
- CubeDimension Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeDimension
helpviewer_keywords:
- CubeDimension data type
ms.assetid: 128ac790-65a1-4e35-b909-8dba2a61b24c
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 4a043895929e09a59d3ae14c5995804c4fa5c7eb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006745"
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|Nenhum|  
|Tipos de dados derivados|Nenhum|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhum|  
|Elementos filho|[AllMemberAggregationUsage](../properties/aggregationusage-element-assl.md), [anotações](../collections/annotations-element-assl.md), [atributos](../collections/attributes-element-assl.md), [DimensionID](../properties/id-element-assl.md), [hierarquias](../collections/hierarchies-element-assl.md), [HierarchyUniqueNameStyle](../properties/hierarchyuniquenamestyle-element-assl.md), [ID](../properties/id-element-assl.md), [MemberUniqueNameStyle](../properties/memberuniquenamestyle-element-assl.md), [nome](../properties/name-element-assl.md), [visível](../properties/visible-element-assl.md), [Traduções](../collections/translations-element-assl.md)|  
|Elementos derivados|[Dimensão](../objects/dimension-element-assl.md) ([dimensões](../collections/dimensions-element-assl.md) coleção de [cubo](../objects/cube-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 Há um elemento `CubeDimension` para cada relação de dimensão em um `Cube`. O elemento `CubeDimension` cobre todos os `MeasureGroups` do cubo.  
  
 Um `CubeDimension` deve incluir um [CubeHierarchy](hierarchy-data-type-assl.md) se a dimensão tiver algo específico a dizer sobre a hierarquia, incluindo a desabilitação da hierarquia (assim, permitindo a seleção das hierarquias aplicáveis a um determinado uso da dimensão), ou fazendo com que a hierarquia invisível.  
  
 Da mesma forma, um `CubeDimension` deve incluir um [CubeAttribute](cubeattribute-data-type-assl.md) somente se a dimensão tiver algo específico a dizer sobre o atributo. Não é possível selecionar os atributos aplicáveis a um uso de dimensão específico, visto que os atributos podem ficar invisíveis.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.CubeDimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  