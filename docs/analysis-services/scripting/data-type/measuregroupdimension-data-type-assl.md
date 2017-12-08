---
title: Tipo de dados MeasureGroupDimension (ASSL) | Microsoft Docs
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
apiname: MeasureGroupDimension Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: MeasureGroupDimension
helpviewer_keywords: MeasureGroupDimension data type
ms.assetid: 9d1c1c19-31ce-4c42-b2e6-4c1b08875a83
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ee6db41fe91e2c680b110ca78374dc8206f2c821
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|Nenhuma|  
|Tipos de dados derivados|[DataMiningMeasureGroupDimension](../../../analysis-services/scripting/data-type/dataminingmeasuregroupdimension-data-type-assl.md), [DegenerateMeasureGroupDimension](../../../analysis-services/scripting/data-type/degeneratemeasuregroupdimension-data-type-assl.md), [ManyToManyMeasureGroupDimension](../../../analysis-services/scripting/data-type/manytomanymeasuregroupdimension-data-type-assl.md), [ReferenceMeasureGroupDimension](../../../analysis-services/scripting/data-type/referencemeasuregroupdimension-data-type-assl.md), [RegularMeasureGroupDimension](../../../analysis-services/scripting/data-type/regularmeasuregroupdimension-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|[Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md), [CubeDimensionID](../../../analysis-services/scripting/properties/cubedimensionid-element-assl.md), [Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|  
|Elementos derivados|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md) (coleção[Dimensions](../../../analysis-services/scripting/collections/dimensions-element-assl.md) de [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md))|  
  
## <a name="remarks"></a>Comentários  
 Cada **MeasureGroupDimension** é uma referência a um das dimensões no cubo. Elas definem quais dimensões de cubo se aplicam ao grupo de medidas.  
  
 O conjunto de atributos fornecidos determina a granularidade (escopo) na qual as medidas do grupo de medidas são conhecidas. Por exemplo, as medidas que representam vendas de produtos estão contidas no grupo de medidas Vendas. As informações dessas medidas são armazenadas na fonte de dados subjacente em uma granularidade mensal, não semanal ou diária. Nesse caso, somente o atributo Mês seria listado para a **MeasureGroupDimension** que descreve a relação entre a dimensão de tempo e o grupo de medidas Vendas. Em casos raros, a granularidade pode ser definida em termos de um conjunto de atributos. Por exemplo, no conjunto de atributos {Dia, Semana, Mês, Ano}, onde Dia implica Semana e Mês, mas Semana não implica Mês, as medidas contidas no grupo de medidas Previsões poderiam ser conhecidas por Mês e Semana, mas não por Dia.  
  
 Se nenhum atributo for fornecido, somente o atributo de chave para a dimensão será listado (definindo o nível mais baixo da granularidade). Cada partição de um grupo de medidas deve ter a mesma granularidade. O conjunto de atributos listado não deve ser redundante com respeito às relações entre atributos. Por exemplo, se Mês implica Ano, a granularidade é definida como Mês, não Mês e Ano.  
  
 Um elemento **MeasureGroupDimension** precisa incluir uma hierarquia somente se tiver algo específico que indicar sobre ela. Não há como selecionar quais hierarquias se aplicam a um grupo de medidas específico. Similarmente, o elemento [MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md) deve ser incluído somente se for necessário indicar algo específico sobre ele.  
  
 Cada hierarquia deve ser um subconjunto das hierarquias incluídas no elemento [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md). Não é possível selecionar os níveis, embora alguns possam ser desabilitados automaticamente de acordo com a granularidade do grupo de medidas.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.MeasureGroupDimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script &#40; do Analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
