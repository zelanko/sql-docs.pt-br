---
title: Elemento KeyColumn (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- KeyColumn Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- KeyColumn
helpviewer_keywords:
- KeyColumn element
ms.assetid: 7b03eeb3-d478-4c38-822e-8cdfcc485039
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 20122b7c8cd12e00d4f89cadba3fd96416756a16
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="keycolumn-element-assl"></a>Elemento KeyColumn (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contém a definição de uma coluna, ou faz parte, a chave para um atributo.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<KeyColumns>  
   <KeyColumn xsi:type="DataItem">...</KeyColumn>  
<KeyColumns>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[O item de dados](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-n: elemento obrigatório que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 Para obter mais informações sobre o **DataItem** tipo, incluindo uma tabela de objetos do Analysis Services Scripting Language (ASSL) e propriedades do **DataItem** de tipo, consulte [tipo de dados de item de dados & #40; ASSL & #41; ](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md).  
  
 Os elementos que correspondem aos pais do **KeyColumns** coleção no modelo de objeto Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.AggregationInstanceAttribute>, <xref:Microsoft.AnalysisServices.DimensionAttribute>, <xref:Microsoft.AnalysisServices.MeasureGroupAttribute>, e <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de dados AggregationInstanceAttribute &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/aggregationinstanceattribute-data-type-assl.md)   
 [Tipo de dados AggregationInstanceCubeDimension &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/aggregationinstancecubedimension-data-type-assl.md)   
 [Tipo de dados DimensionAttribute &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)   
 [Tipo de dados MeasureGroupAttribute &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)   
 [Tipo de dados ScalarMiningStructureColumn &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)   
 [Objetos de & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
