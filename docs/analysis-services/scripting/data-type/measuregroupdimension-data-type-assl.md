---
title: Tipo de dados MeasureGroupDimension (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e449579bc1544f0cc26f181dc67dbec5f9e00f2f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34037217"
---
# <a name="measuregroupdimension-data-type-assl"></a>Tipo de dados MeasureGroupDimension (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
## <a name="remarks"></a>Remarks  
 Cada **MeasureGroupDimension** é uma referência a um das dimensões no cubo. Elas definem quais dimensões de cubo se aplicam ao grupo de medidas.  
  
 O conjunto de atributos fornecidos determina a granularidade (escopo) na qual as medidas do grupo de medidas são conhecidas. Por exemplo, as medidas que representam vendas de produtos estão contidas no grupo de medidas Vendas. As informações dessas medidas são armazenadas na fonte de dados subjacente em uma granularidade mensal, não semanal ou diária. Nesse caso, somente o atributo Mês seria listado para a **MeasureGroupDimension** que descreve a relação entre a dimensão de tempo e o grupo de medidas Vendas. Em casos raros, a granularidade pode ser definida em termos de um conjunto de atributos. Por exemplo, no conjunto de atributos {Dia, Semana, Mês, Ano}, onde Dia implica Semana e Mês, mas Semana não implica Mês, as medidas contidas no grupo de medidas Previsões poderiam ser conhecidas por Mês e Semana, mas não por Dia.  
  
 Se nenhum atributo for fornecido, somente o atributo de chave para a dimensão será listado (definindo o nível mais baixo da granularidade). Cada partição de um grupo de medidas deve ter a mesma granularidade. O conjunto de atributos listado não deve ser redundante com respeito às relações entre atributos. Por exemplo, se Mês implica Ano, a granularidade é definida como Mês, não Mês e Ano.  
  
 Um elemento **MeasureGroupDimension** precisa incluir uma hierarquia somente se tiver algo específico que indicar sobre ela. Não há como selecionar quais hierarquias se aplicam a um grupo de medidas específico. Similarmente, o elemento [MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md) deve ser incluído somente se for necessário indicar algo específico sobre ele.  
  
 Cada hierarquia deve ser um subconjunto das hierarquias incluídas no elemento [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md). Não é possível selecionar os níveis, embora alguns possam ser desabilitados automaticamente de acordo com a granularidade do grupo de medidas.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.MeasureGroupDimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script & #40; do Analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
