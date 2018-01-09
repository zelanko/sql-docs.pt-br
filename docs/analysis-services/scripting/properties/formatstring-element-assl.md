---
title: Elemento FormatString (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: FormatString Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: FormatString
helpviewer_keywords: FormatString element
ms.assetid: 7b996221-936e-4f36-a3a8-676eb9869c55
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e4194f090eb29b61ecd0c6dff84883d7b790e7e2
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="formatstring-element-assl"></a>Elemento FormatString (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Descreve o formato de exibição para um [CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md) elemento ou um [medidas](../../../analysis-services/scripting/objects/measure-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CalculationProperty> <!-- or Measure -->  
   ...  
   <FormatString>...</FormatString>  
   ...  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md), [medidas](../../../analysis-services/scripting/objects/measure-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 A propriedade **FormatString** contém uma linguagem MDX. No caso de **CalculationProperty** elementos, ela se aplica aos elementos com um [CalculationType](../../../analysis-services/scripting/properties/calculationtype-element-assl.md) de *membro* ou *células*.  
  
 Os elementos que correspondem aos pais de **FormatString** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.CalculationProperty> e <xref:Microsoft.AnalysisServices.Measure>.  
  
## <a name="see-also"></a>Consulte Também  
 [Elemento CalculationProperties &#40; ASSL &#41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)   
 [Elemento MdxScript &#40; ASSL &#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)   
 [Elemento MdxScripts &#40; ASSL &#41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
