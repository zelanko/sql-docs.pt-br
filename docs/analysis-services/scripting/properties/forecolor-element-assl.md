---
title: Elemento ForeColor (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- ForeColor Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ForeColor
helpviewer_keywords:
- ForeColor element
ms.assetid: 5125520c-3bce-40e6-a722-8d4d47306fed
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 5f711707139ba275378cded9a067679a94342485
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="forecolor-element-assl"></a>Elemento ForeColor (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Descreve características de exibição relacionadas à cor do [CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md) ou [medidas](../../../analysis-services/scripting/objects/measure-element-assl.md) elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CalculationProperty> <!-- or Measure -->  
   ...  
   <ForeColor>...</ForeColor>  
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
  
## <a name="remarks"></a>Remarks  
 O **ForeColor** propriedade contém uma expressão MDX (Multidimensional Expressions) e se aplica a **CalculationProperty** elementos que têm um [CalculationType](../../../analysis-services/scripting/properties/calculationtype-element-assl.md) de *Membro* ou *células*.  
  
 Os elementos que correspondem aos pais de **ForeColor** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.CalculationProperty> e <xref:Microsoft.AnalysisServices.Measure>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento CalculationProperties &#40;ASSL&#41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)   
 [Elemento MdxScript &#40;ASSL&#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)   
 [Elemento MdxScripts &#40;ASSL&#41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)   
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
