---
title: Tipo de dados DegenerateMeasureGroupDimension (ASSL) | Microsoft Docs
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
- DegenerateMeasureGroupDimension Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DegenerateMeasureGroupDimension
helpviewer_keywords:
- DegenerateMeasureGroupDimension data type
ms.assetid: a64fe908-154d-4fea-b435-afb6ee37a6fa
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 343668137e77f53f94df2b6bc1324c3a67d94256
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37321138"
---
# <a name="degeneratemeasuregroupdimension-data-type-assl"></a>Tipo de dados DegenerateMeasureGroupDimension (ASSL)
  Define um tipo de dados derivado que representa a relação entre uma dimensão de degeneração (ou seja, uma dimensão de fatos) e um grupo de medidas.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DegenerateMeasureGroupDimension>  
   <!-- DegenerateMeasureGroupDimension does not have any elements that extend RegularMeasureGroupDimension -->  
</DegenerateMeasureGroupDimension>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|[RegularMeasureGroupDimension](dimension-data-type-assl.md)|  
|Tipos de dados derivados|Nenhum|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhum|  
|Elementos filho|Nenhum|  
|Elementos derivados|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Para obter mais informações sobre dimensões de fato, consulte [relações de dimensão](../../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.DegenerateMeasureGroupDimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
