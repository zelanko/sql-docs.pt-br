---
title: Tipo de dados RelationshipEnd (ASSL) | Microsoft Docs
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
ms.assetid: 3a974dd4-e1d6-45b2-b8c8-1a914bc13a02
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0f201bd910b9fd7f07b04a9b9f30da659dd32f29
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118526"
---
# <a name="relationshipend-data-type-assl"></a>Tipo de dados RelationshipEnd (ASSL)
  Define um tipo de dados primitivo que representa uma extremidade em uma relação.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<RelationshipEnd>  
   <Role>...</Role>  
   <Multiplicity>...</Multiplicity>  
   <DimensionID>...</DimensionID>  
   <Attributes>...</Attributes>  
   <Translations>...</Translations>  
   <VisualizationProperties>...</VisualizationProperties>  
</Relationship>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|Nenhum|  
|Tipos de dados derivados|Nenhum|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Relação](relationship-data-type-assl.md)|  
|Elementos filho|[Função](../../xmla/xml-elements-properties/role-element-xmla.md), [Multiplicidade](../properties/multiplicity-element-assl.md), [DimensionID](../properties/id-element-assl.md), [Atributos](../collections/attributes-element-assl.md), [Traduções](../collections/translations-element-assl.md), [VisualizationProperties](relationshipendvisualizationproperties-data-type-assl.md)|  
|Elementos derivados||  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.RelationshipEnd>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  