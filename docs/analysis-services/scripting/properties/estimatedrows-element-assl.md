---
title: Elemento EstimatedRows (ASSL) | Microsoft Docs
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
apiname: EstimatedRows Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: EstimatedRows
helpviewer_keywords: EstimatedRows element
ms.assetid: 08a66481-6479-4a93-aa7e-15e8b1f854f2
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 87433d1bdd8b246ab13e7562d0fa19d0a66934b1
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="estimatedrows-element-assl"></a>Elemento EstimatedRows (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém o número estimado de linhas representado pelo elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AggregationDesign> <!-- or Cube, MeasureGroup, MeasureGroupBinding, Partition -->  
   ...  
   <EstimatedRows>...</EstimatedRows>  
   ...  
</AggregationDimension>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Longo|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md), [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md), [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md), [partição](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Os elementos que correspondem aos pais de **EstimatedRows** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.AggregationDesign>, <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.MeasureGroup>, <xref:Microsoft.AnalysisServices.MeasureGroupBinding>, e <xref:Microsoft.AnalysisServices.Partition>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
