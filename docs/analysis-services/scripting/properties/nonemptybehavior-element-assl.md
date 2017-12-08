---
title: Elemento NonEmptyBehavior (ASSL) | Microsoft Docs
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
apiname: NonEmptyBehavior Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: NonEmptyBehavior
helpviewer_keywords: NonEmptyBehavior element
ms.assetid: b4c78af4-b049-4189-a35b-206e3938d1db
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7cfa1c3e23d5868c936947fe0ef6b30ae3a5fcdc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="nonemptybehavior-element-assl"></a>Elemento NonEmptyBehavior (ASSL)
  Determina o comportamento não vazio associado com o pai do [CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CalculationProperty>  
  
   <NonEmptyBehavior>...</NonEmptyBehavior>  
  
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
|Elemento pai|[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O **NonEmptyBehavior** propriedade se aplica a **CalculationProperty** elementos com um [CalculationType](../../../analysis-services/scripting/properties/calculationtype-element-assl.md) definida como *membro*.  
  
 O elemento que corresponde ao pai do **NonEmptyBehavior** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.CalculationProperty>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento CalculationProperties &#40; ASSL &#41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)   
 [Elemento MdxScript &#40; ASSL &#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)   
 [Elemento MdxScripts &#40; ASSL &#41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
