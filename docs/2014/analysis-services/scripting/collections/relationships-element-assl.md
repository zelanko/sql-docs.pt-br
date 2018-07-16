---
title: Elemento Relationships (ASSL) | Microsoft Docs
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
ms.assetid: e78882c9-b14e-4044-848e-ea7fddd3b75d
caps.latest.revision: 6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2071ae26b20ee39b47115e4ada1695878631fc84
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37316946"
---
# <a name="relationships-element-assl"></a>Elemento Relationships (ASSL)
  Contém a coleção de relações para a dimensão associada.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CubeDimension> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Attributes>  
      <Attribute>...</Attribute>  
  </Attributes>  
   ...  
</CubeDimension>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[CubeDimension](../data-type/dimension-data-type-assl.md), [dimensão](../objects/dimension-element-assl.md), [PerspectiveDimension](../data-type/perspectivedimension-data-type-assl.md), [RegularMeasureGroupDimension](../data-type/measuregroupdimension-data-type-assl.md)|  
|Elementos filho|[Relação](../data-type/relationship-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Os elementos correspondentes no modelo de objeto Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.RelationshipCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Coleções &#40;ASSL&#41;](collections-assl.md)  
  
  
