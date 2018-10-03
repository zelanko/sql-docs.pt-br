---
title: Elemento KeyColumn (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- KeyColumn Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- KeyColumn
helpviewer_keywords:
- KeyColumn element
ms.assetid: 7b03eeb3-d478-4c38-822e-8cdfcc485039
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1cc42afde5212befbbd2a16a81340fb7e1f629bb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48090297"
---
# <a name="keycolumn-element-assl"></a>Elemento KeyColumn (ASSL)
  Contém a definição de uma coluna que é ou faz parte, a chave para um atributo.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<KeyColumns>  
   <KeyColumn xsi:type="DataItem">...</KeyColumn>  
<KeyColumns>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|Valor padrão|None|  
|Cardinalidade|1-n: elemento obrigatório que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[KeyColumns](../collections/columns-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre o `DataItem` tipo, incluindo uma tabela de objetos do Analysis Services Scripting Language (ASSL) e propriedades do `DataItem` de tipo, consulte [tipo de dados DataItem &#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md).  
  
 Os elementos que correspondem aos pais da coleção `KeyColumns` no modelo de objeto AMO (Objetos de Gerenciamento de Análise) são <xref:Microsoft.AnalysisServices.AggregationInstanceAttribute>, <xref:Microsoft.AnalysisServices.DimensionAttribute>, <xref:Microsoft.AnalysisServices.MeasureGroupAttribute> e <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de dados AggregationInstanceAttribute &#40;ASSL&#41;](../data-type/aggregationinstanceattribute-data-type-assl.md)   
 [Tipo de dados AggregationInstanceCubeDimension &#40;ASSL&#41;](../data-type/dimension-data-type-assl.md)   
 [Tipo de dados DimensionAttribute &#40;ASSL&#41;](../data-type/dimensionattribute-data-type-assl.md)   
 [Tipo de dados MeasureGroupAttribute &#40;ASSL&#41;](../data-type/measuregroupattribute-data-type-assl.md)   
 [Tipo de dados ScalarMiningStructureColumn &#40;ASSL&#41;](../data-type/miningstructurecolumn-data-type-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
