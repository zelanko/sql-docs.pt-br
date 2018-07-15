---
title: Elemento MeasureID (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MeasureID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MeasureID
helpviewer_keywords:
- MeasureID element
ms.assetid: 8457aebc-8fdd-4683-8640-baaf9d89b2a2
caps.latest.revision: 32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d7a1ff1e817ae78307f8da134e88e742295892ba
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37326526"
---
# <a name="measureid-element-assl"></a>Elemento MeasureID (ASSL)
  Associa um [medida](../objects/measure-element-assl.md) elemento com o elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MeasureBinding> <!-- or AggregationInstanceMeasure, PerspectiveMeasure -->  
   ...  
   <MeasureID>...</MeasureID>  
   ...  
</MeasureBinding>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[AggregationInstanceMeasure](../data-type/aggregationinstancemeasure-data-type-assl.md), [MeasureBinding](../data-type/binding-data-type-assl.md), [PerspectiveMeasure](../data-type/perspectivemeasure-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Os elementos que correspondem aos pais de `MeasureID` no modelo de objeto AMO (Objetos de Gerenciamento de Análise) são <xref:Microsoft.AnalysisServices.AggregationInstanceMeasure>, <xref:Microsoft.AnalysisServices.MeasureBinding> e <xref:Microsoft.AnalysisServices.PerspectiveMeasure>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
