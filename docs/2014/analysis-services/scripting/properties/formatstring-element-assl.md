---
title: Elemento FormatString (ASSL) | Microsoft Docs
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
- FormatString Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- FormatString
helpviewer_keywords:
- FormatString element
ms.assetid: 7b996221-936e-4f36-a3a8-676eb9869c55
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0760432767a8f7fb1dcdec99c2ca7d76722ddb38
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010759"
---
# <a name="formatstring-element-assl"></a>Elemento FormatString (ASSL)
  Descreve o formato de exibição para um [CalculationProperty](../objects/calculationproperty-element-assl.md) elemento ou um [medidas](../objects/measure-element-assl.md) elemento.  
  
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
|Elementos pai|[CalculationProperty](../objects/calculationproperty-element-assl.md), [medidas](../objects/measure-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 A propriedade `FormatString` contém uma linguagem MDX. No caso de `CalculationProperty` elementos, ela se aplica aos elementos com um [CalculationType](calculationtype-element-assl.md) de *membro* ou *células*.  
  
 Os elementos que correspondem aos pais de `FormatString` no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.CalculationProperty> e <xref:Microsoft.AnalysisServices.Measure>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento CalculationProperties &#40;ASSL&#41;](../collections/calculationproperties-element-assl.md)   
 [Elemento MdxScript &#40;ASSL&#41;](../objects/mdxscript-element-assl.md)   
 [Elemento MdxScripts &#40;ASSL&#41;](../collections/mdxscripts-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  