---
title: Elemento HierarchyUniqueNameStyle (ASSL) | Microsoft Docs
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
apiname:
- HierarchyUniqueNameStyle Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- HierarchyUniqueNameStyle element
ms.assetid: 2ac57825-e9e5-4ec4-9856-fa2326d2c43f
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e19b3e412b7330d6ef735bf269b72080e031b024
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="hierarchyuniquenamestyle-element-assl"></a>Elemento HierarchyUniqueNameStyle (ASSL)
  Determina como nomes exclusivos são gerados para hierarquias que estão contidas dentro do [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CubeDimension>  
   ...  
   <HierarchyUniqueNameStyle>...</HierarchyUniqueNameStyle>  
   ...  
</CubeDimension>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*IncludeDimensionName*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*IncludeDimensionName*|O nome da dimensão é incluído como parte do nome da hierarquia.|  
|*ExcludeDimensionName*|O nome da dimensão não é incluído como parte do nome da hierarquia.|  
  
 O elemento que corresponde ao pai do **HierarchyUniqueNameStyle** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.CubeDimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Cube &#40; ASSL &#41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [Elemento Dimension &#40; ASSL &#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

