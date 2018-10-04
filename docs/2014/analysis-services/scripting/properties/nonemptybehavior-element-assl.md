---
title: Elemento NonEmptyBehavior (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- NonEmptyBehavior Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- NonEmptyBehavior
helpviewer_keywords:
- NonEmptyBehavior element
ms.assetid: b4c78af4-b049-4189-a35b-206e3938d1db
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 911b797b3f1d6ff2a8cd9fac1dfc88384d2cac7f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227976"
---
# <a name="nonemptybehavior-element-assl"></a>Elemento NonEmptyBehavior (ASSL)
  Determina o comportamento não vazio associado ao pai do [CalculationProperty](../objects/calculationproperty-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CalculationProperty>  
  
   <NonEmptyBehavior>...</NonEmptyBehavior>  
  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|None|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[CalculationProperty](../objects/calculationproperty-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O `NonEmptyBehavior` propriedade se aplica ao `CalculationProperty` elementos com um [CalculationType](calculationtype-element-assl.md) definido como *membro*.  
  
 O elemento que corresponde ao pai de `NonEmptyBehavior` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.CalculationProperty>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento CalculationProperties &#40;ASSL&#41;](../collections/calculationproperties-element-assl.md)   
 [Elemento MdxScript &#40;ASSL&#41;](../objects/mdxscript-element-assl.md)   
 [Elemento MdxScripts &#40;ASSL&#41;](../collections/mdxscripts-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
