---
title: Elemento SourceMeasureGroup (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: SourceMeasureGroup Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: SourceMeasureGroup
helpviewer_keywords: SourceMeasureGroup element
ms.assetid: aaa7cc0b-162a-4c31-ab03-a90f81eeca00
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 76f5d0ad24e76484f50598af9f06f6b13331c43f
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="sourcemeasuregroup-element-assl"></a>Elemento SourceMeasureGroup (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Identifica o grupo de medidas que serve como a fonte de dados para uma coluna de estrutura de mineração.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MiningStructureColumn xsi:type="TableMiningStructureColumn">  
   ...  
   <SourceMeasureGroup xsi:type="MeasureGroupBinding">...</SourceMeasureGroup>  
   ...  
</MiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md) do tipo [TableMiningStructureColumn](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre o **associação** tipo, incluindo tabelas de objetos do Analysis Services Scripting Language (ASSL) da **associação** tipo e a hierarquia de herança de **de associação**  tipos, consulte [associação de tipo de dados &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 Para obter uma visão geral de associações de dados em ASSL, consulte [fontes de dados e associações &#40; SSAS Multidimensional &#41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 Os elementos que correspondem aos pais de **SourceMeasureGroup** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.MiningStructureColumn> e <xref:Microsoft.AnalysisServices.TableMiningStructureColumn>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
