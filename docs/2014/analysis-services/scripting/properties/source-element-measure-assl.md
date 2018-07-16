---
title: Elemento (Measure) (ASSL) de origem | Microsoft Docs
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
- Source Element (Measure)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Source
helpviewer_keywords:
- Source element
ms.assetid: 9bae7ba4-3065-4623-b3e0-d54cebea7503
caps.latest.revision: 32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7d4e374490fdfe04e5da39a0f4e9424b2cb1ccde
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37323206"
---
# <a name="source-element-measure-assl"></a>Elemento Source (Measure) (ASSL)
  Contém os detalhes da origem que contém o valor de [medida](../objects/measure-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Measure>  
      ...  
   <Source xsi:type="DataItem">...</Source>  
      ...  
</Measure>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Medida](../objects/measure-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O `Source` do `DataItem`, que serve como o `Source` da `Measure`, por sua vez pode ser do tipo [RowBinding](../data-type/binding-data-type-assl.md), [ColumnBinding](../data-type/columnbinding-data-type-assl.md), [MeasureBinding ](../data-type/measurebinding-data-type-assl.md), ou [CubeDimensionBinding](../data-type/dimensionbinding-data-type-assl.md).  
  
 Para obter mais informações sobre o `DataItem` tipo, incluindo uma tabela de objetos ASSL e as propriedades do `DataItem` de tipo, consulte [tipo de dados DataItem &#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md).  
  
 O elemento que corresponde ao pai de `Source` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Measure>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
