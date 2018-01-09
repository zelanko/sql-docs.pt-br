---
title: Elemento Visible (ASSL) | Microsoft Docs
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
apiname: Visible Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Visible
helpviewer_keywords: Visible element
ms.assetid: 3e9baf1b-351f-4ebf-b57d-13d561f72d6f
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8557812e04b9f91be4beca24113ddf05ff8def64
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="visible-element-assl"></a>Elemento Visible (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Determina a visibilidade do elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CalculationProperty> <!-- or one of the elements listed below in the Element Relationships table -->  
  
   <Visible >...</Visible >  
  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Booliano|  
|Valor padrão|True|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md), [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md), [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md), [CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md), [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md), [ Medida](../../../analysis-services/scripting/objects/measure-element-assl.md), [MemberProperty](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O elemento **Visible** determina se os componentes da interface de usuário devem exibir o elemento pai.  
  
 Os elementos que correspondem aos pais de **visível** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.CalculationProperty>, <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.CubeDimension>, <xref:Microsoft.AnalysisServices.CubeHierarchy>, <xref:Microsoft.AnalysisServices.Database>, e <xref:Microsoft.AnalysisServices.Measure>.  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
