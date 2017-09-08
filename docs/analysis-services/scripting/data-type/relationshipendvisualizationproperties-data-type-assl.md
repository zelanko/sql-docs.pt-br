---
title: Tipo de dados RelationshipEndVisualizationProperties (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 11f9a10f-d36c-4faf-b595-3fe969d1935e
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9627f9a245230f13030b87ae63df47ec920c271a
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="relationshipendvisualizationproperties-data-type-assl"></a>Tipo de dados RelationshipEndVisualizationProperties (ASSL)
  Define um tipo de dados primitivo que representa uma extremidade em uma relação.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<RelationshipEnd>  
   <FolderPosition>...</FolderPosition>  
   <ContextualNameRule>...</ContextualNameRule>  
   <DefaultDetailsPosition>...</DefaultDetailsPosition>  
   <DisplayKeyPosition>...</DisplayKeyPosition>  
   <CommonIdentifierPosition>...</CommonIdentifierPosition>  
   <IsDefaultMeasure>...</IsDefaultMeasure>  
   <IsDefaultImage>...</IsDefaultImage>  
   <SortPropertiesPosition>...</SortPropertiesPosition>  
</RelationshipEnd>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|Nenhuma|  
|Tipos de dados derivados|Nenhuma|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[RelationshipEnd](../../../analysis-services/scripting/data-type/relationshipend-data-type-assl.md)|  
|Elementos filho|[FolderPosition](../../../analysis-services/xmla/xml-elements-properties/folderposition-element-xml.md), [ContextualNameRule](../../../analysis-services/xmla/xml-elements-properties/contextualnamerule-element-xml.md), [DefaultDetailsPosition](../../../analysis-services/xmla/xml-elements-properties/defaultdetailsposition-element-xml.md), [DisplayKeyPosition](../../../analysis-services/xmla/xml-elements-properties/displaykeyposition-element-xml.md), [CommonIdentifierPosition](../../../analysis-services/xmla/xml-elements-properties/commonidentifierposition-element-xml.md), [IsDefaultMeasure](../../../analysis-services/xmla/xml-elements-properties/isdefaultmeasure-element-xml.md), [IsDefaultImage](../../../analysis-services/xmla/xml-elements-properties/isdefaultimage-element-xml.md), [SortPropertiesPosition](../../../analysis-services/xmla/xml-elements-properties/sortpropertiesposition-element-xml.md)|  
|Elementos derivados||  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.RelationshipEnd>.  
  
  
