---
title: Elemento EstimatedCount (ASSL) | Microsoft Docs
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
- EstimatedCount Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- EstimatedCount
helpviewer_keywords:
- EstimatedCount element
ms.assetid: ce84b54a-8ab2-42f4-a7dd-e10a3d41cb4d
caps.latest.revision: 32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a69d67554d0090e0e586421986bc97ba556c84a4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37300846"
---
# <a name="estimatedcount-element-assl"></a>Elemento EstimatedCount (ASSL)
  Contém o número estimado de membros para um atributo, conforme definido pelo usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AggregationDesignAttribute> <!-- or DimensionAttribute -->  
      ...  
   <EstimatedCount>...</EstimatedCount>  
   ...  
</AggregationDesignAttribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Longo|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[AggregationDesignAttribute](../data-type/aggregationdesignattribute-data-type-assl.md), [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Esse valor é atribuído pelo usuário e é usado pelas [elemento AggregationDesign &#40;ASSL&#41;](../objects/aggregationdesign-element-assl.md).  
  
 Os elementos que correspondem aos pais de `EstimatedCount` no modelo de objeto Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.AggregationDesignAttribute> e <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
