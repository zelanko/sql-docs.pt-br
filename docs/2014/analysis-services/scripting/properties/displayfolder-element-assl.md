---
title: Elemento DisplayFolder (ASSL) | Microsoft Docs
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
- DisplayFolder Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DisplayFolder
helpviewer_keywords:
- DisplayFolder element
ms.assetid: 55184c02-03e7-4d6c-b87a-d4d34bc11d0e
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c959f1c2fe298217b46849c6a13d3e0f313f6803
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012580"
---
# <a name="displayfolder-element-assl"></a>Elemento DisplayFolder (ASSL)
  Especifica a pasta na qual listar o elemento pai. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] aplicativos para desenvolvedores e administradores podem oferecer suporte o uso de pastas de exibição para categorizar vários elementos visualmente.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CalculationProperty> <!-- or Hierarchy, Kpi, Measure, Translation -->  
   ...  
   <DisplayFolder>...</DisplayFolder>  
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
|Elementos pai|[CalculationProperty](../objects/calculationproperty-element-assl.md), [hierarquia](../objects/hierarchy-element-assl.md), [Kpi](../objects/kpi-element-assl.md), [medidas](../objects/measure-element-assl.md), [tradução](../objects/translation-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Em cubos maiores, pode haver centenas de medidas e hierarquias. A propriedade `DisplayFolder` define a aparência de usuário no cliente. O valor da propriedade `DisplayFolder` pode conter qualquer uma das opções a seguir:  
  
-   Estar vazia, indicando que a medida não pertence a uma pasta.  
  
-   Conter um único nome de pasta, indicando que a medida deve ser processada como pertencente a uma pasta com o mesmo nome.  
  
-   Contém vários nomes de pasta separados por uma barra invertida (\\), indicando uma hierarquia de pasta inserido.  
  
 O `DisplayFolder` propriedade se aplica a `CalculationProperty` se somente elementos o valor de [CalculationType](calculationtype-element-assl.md) é definido como *membro*.  
  
 Os elementos que correspondem aos pais de `DisplayFolder` no modelo de objeto AMO (Objetos de Gerenciamento de Análise)são <xref:Microsoft.AnalysisServices.CalculationProperty>, <xref:Microsoft.AnalysisServices.Hierarchy>, <xref:Microsoft.AnalysisServices.Kpi>, <xref:Microsoft.AnalysisServices.Measure> e <xref:Microsoft.AnalysisServices.Translation>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento CalculationProperties &#40;ASSL&#41;](../collections/calculationproperties-element-assl.md)   
 [Elemento MdxScript &#40;ASSL&#41;](../objects/mdxscript-element-assl.md)   
 [Elemento MdxScripts &#40;ASSL&#41;](../collections/mdxscripts-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  