---
title: Elemento FontSize (ASSL) | Microsoft Docs
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
apiname: FontSize Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: FontSize
helpviewer_keywords: FontSize element
ms.assetid: 49f66a73-946a-4fbd-9749-a3ca1b717ff3
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 170c1ecf03be938c4a39da3709e0c03956bbfe29
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="fontsize-element-assl"></a>Elemento FontSize (ASSL)
  Descreve características de exibição relacionadas à fonte de [CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md) ou [medidas](../../../analysis-services/scripting/objects/measure-element-assl.md) elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CalculationProperty> <!-- or Measure -->  
   ...  
   <FontSize>...</FontSize>  
   ...  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md), [medidas](../../../analysis-services/scripting/objects/measure-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O **FontSize** propriedade contém uma expressão MDX (Multidimensional Expressions) e se aplica a **CalculationProperty** elementos que têm um [CalculationType](../../../analysis-services/scripting/properties/calculationtype-element-assl.md) de *Membro* ou *células*.  
  
 Os elementos que correspondem aos pais de **FontSize** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.CalculationProperty> e <xref:Microsoft.AnalysisServices.Measure>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento CalculationProperties &#40; ASSL &#41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)   
 [Elemento MdxScript &#40; ASSL &#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)   
 [Elemento MdxScripts &#40; ASSL &#41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
