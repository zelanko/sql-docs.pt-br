---
title: Tipo de dados MeasureGroupDimension (ASSL) | Microsoft Docs
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
- MeasureGroupDimension Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MeasureGroupDimension
helpviewer_keywords:
- MeasureGroupDimension data type
ms.assetid: 9d1c1c19-31ce-4c42-b2e6-4c1b08875a83
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3dcbba7071e1f2efc8ede59259a48a334652de81
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37249116"
---
# <a name="measuregroupdimension-data-type-assl"></a>Tipo de dados MeasureGroupDimension (ASSL)
  Define um tipo de dados primitivo abstrato que representa a relação entre uma dimensão e um grupo de medidas.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MeasureGroupDimension>  
   <CubeDimensionID>...</CubeDimensionID>  
      <Annotations>...</Annotations>  
   <Source>...</Source>  
</MeasureGroupDimension>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|Nenhum|  
|Tipos de dados derivados|[DataMiningMeasureGroupDimension](dimension-data-type-assl.md), [DegenerateMeasureGroupDimension](measuregroupdimension-data-type-assl.md), [ManyToManyMeasureGroupDimension](manytomanymeasuregroupdimension-data-type-assl.md), [ReferenceMeasureGroupDimension](referencemeasuregroupdimension-data-type-assl.md), [RegularMeasureGroupDimension](regularmeasuregroupdimension-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhum|  
|Elementos filho|[Annotations](../collections/annotations-element-assl.md), [CubeDimensionID](../properties/id-element-assl.md), [Source](../properties/source-element-binding-assl.md)|  
|Elementos derivados|[Dimension](../objects/dimension-element-assl.md) (coleção[Dimensions](../collections/dimensions-element-assl.md) de [MeasureGroup](../objects/group-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 Cada `MeasureGroupDimension` é uma referência a um das dimensões no cubo. Elas definem quais dimensões de cubo se aplicam ao grupo de medidas.  
  
 O conjunto de atributos fornecidos determina a granularidade (escopo) na qual as medidas do grupo de medidas são conhecidas. Por exemplo, as medidas que representam vendas de produtos estão contidas no grupo de medidas Vendas. As informações dessas medidas são armazenadas na fonte de dados subjacente em uma granularidade mensal, não semanal ou diária. Nesse caso, somente o atributo Mês seria listado para a `MeasureGroupDimension` que descreve a relação entre a dimensão de tempo e o grupo de medidas Vendas. Em casos raros, a granularidade pode ser definida em termos de um conjunto de atributos. Por exemplo, no conjunto de atributos {Dia, Semana, Mês, Ano}, onde Dia implica Semana e Mês, mas Semana não implica Mês, as medidas contidas no grupo de medidas Previsões poderiam ser conhecidas por Mês e Semana, mas não por Dia.  
  
 Se nenhum atributo for fornecido, somente o atributo de chave para a dimensão será listado (definindo o nível mais baixo da granularidade). Cada partição de um grupo de medidas deve ter a mesma granularidade. O conjunto de atributos listado não deve ser redundante com respeito às relações entre atributos. Por exemplo, se Mês implica Ano, a granularidade é definida como Mês, não Mês e Ano.  
  
 Um elemento `MeasureGroupDimension` precisa incluir uma hierarquia somente se tiver algo específico que indicar sobre ela. Não há como selecionar quais hierarquias se aplicam a um grupo de medidas específico. Similarmente, o elemento [MeasureGroupAttribute](measuregroupattribute-data-type-assl.md) deve ser incluído somente se for necessário indicar algo específico sobre ele.  
  
 Cada hierarquia deve ser um subconjunto das hierarquias incluídas no elemento [CubeDimension](cubedimension-data-type-assl.md). Não é possível selecionar os níveis, embora alguns possam ser desabilitados automaticamente de acordo com a granularidade do grupo de medidas.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.MeasureGroupDimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
