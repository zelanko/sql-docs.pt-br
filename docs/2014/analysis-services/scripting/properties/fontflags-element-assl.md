---
title: Elemento FontFlags (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- FontFlags Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- FontFlags
helpviewer_keywords:
- FontFlags element
ms.assetid: ea608da9-ab05-42ab-8872-c52cd9f3f546
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c1896d01c47f7c2e2fa4289f09c10ef859eff1d4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37156837"
---
# <a name="fontflags-element-assl"></a>Elemento FontFlags (ASSL)
  Descreve características de exibição relacionadas à fonte de [CalculationProperty](../objects/calculationproperty-element-assl.md) ou [medida](../objects/measure-element-assl.md) elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CalculationProperty> <!-- or Measure -->  
   ...  
      <FontFlags>...</FontFlags>  
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
|Elementos pai|[CalculationProperty](../objects/calculationproperty-element-assl.md), [medidas](../objects/measure-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O `FontFlags` propriedade contém uma expressão MDX (Multidimensional Expressions) e aplica-se ao `CalculationProperty` elementos que têm um [CalculationType](calculationtype-element-assl.md) dos *membro* ou *células* .  
  
 Os elementos que correspondem aos pais de `FontFlags` no modelo de objeto Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.CalculationProperty> e <xref:Microsoft.AnalysisServices.Measure>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento CalculationProperties &#40;ASSL&#41;](../collections/calculationproperties-element-assl.md)   
 [Elemento MdxScript &#40;ASSL&#41;](../objects/mdxscript-element-assl.md)   
 [Elemento MdxScripts &#40;ASSL&#41;](../collections/mdxscripts-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
