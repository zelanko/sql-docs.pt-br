---
title: Elemento DisplayFolder (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6986e1dc728591f9540b533052ef8fd135aca1b0
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="displayfolder-element-assl"></a>Elemento DisplayFolder (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md), [hierarquia](../../../analysis-services/scripting/objects/hierarchy-element-assl.md), [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md), [medidas](../../../analysis-services/scripting/objects/measure-element-assl.md), [tradução](../../../analysis-services/scripting/objects/translation-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 Em cubos maiores, pode haver centenas de medidas e hierarquias. A propriedade **DisplayFolder** define a aparência de usuário no cliente. O valor da propriedade **DisplayFolder** pode conter qualquer uma das opções a seguir:  
  
-   Estar vazia, indicando que a medida não pertence a uma pasta.  
  
-   Conter um único nome de pasta, indicando que a medida deve ser processada como pertencente a uma pasta com o mesmo nome.  
  
-   Contém vários nomes de pasta separados por uma barra invertida (\\), indicando uma hierarquia de pasta inserido.  
  
 O **DisplayFolder** propriedade se aplica a **CalculationProperty** se somente elementos o valor de [CalculationType](../../../analysis-services/scripting/properties/calculationtype-element-assl.md) é definido como *membro* .  
  
 Os elementos que correspondem aos pais de **DisplayFolder** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.CalculationProperty>, <xref:Microsoft.AnalysisServices.Hierarchy>, <xref:Microsoft.AnalysisServices.Kpi>, <xref:Microsoft.AnalysisServices.Measure>, e <xref:Microsoft.AnalysisServices.Translation>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento CalculationProperties &#40;ASSL&#41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)   
 [Elemento MdxScript &#40;ASSL&#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)   
 [Elemento MdxScripts &#40;ASSL&#41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)   
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
