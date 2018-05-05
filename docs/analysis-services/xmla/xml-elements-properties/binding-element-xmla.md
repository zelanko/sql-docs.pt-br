---
title: Elemento Binding (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Binding Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.binding
- http://schemas.microsoft.com/analysisservices/2003/engine#Binding
- urn:schemas-microsoft-com:xml-analysis#Binding
helpviewer_keywords:
- Binding element
ms.assetid: d5acd8d4-8551-449a-ae30-d0ba828cc02d
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0b7ac8ef65b5a4d05dc0ac6fe688aeaea8c2cf59
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="binding-element-xmla"></a>Elemento Binding (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Define uma associação fora de linha para um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] objeto, como um atributo em uma dimensão, para o [associações](../../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md) coleção de um [lote](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) ou [ Processo](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) comando.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Bindings>  
   <Binding xsi:type="DimensionAttributeBinding">...</Binding>  
   <!-- or -->  
   <Binding xsi:type="MeasureGroupAttributeBinding">...</Binding>  
   <!-- or -->  
   <Binding xsi:type="PartitionBinding">...</Binding>  
</Bindings>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[DimensionAttributeBinding](../../../analysis-services/scripting/data-type/dimensionattributebinding-data-type-out-of-line-assl.md), [MeasureGroupAttributeBinding](../../../analysis-services/scripting/data-type/measuregroupattributebinding-data-type-out-of-line-assl.md), [PartitionBinding](../../../analysis-services/scripting/data-type/partitionbinding-data-type-assl.md)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Associações](../../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 **Associação** elementos definem associações fora de linha, diferentes fontes de dados e exibições da fonte de dados, para [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] objetos a serem processados por um **lote** ou **processo** comando. Para obter mais informações sobre o processamento de objetos, consulte [processar objetos &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md).  
  
 Para obter mais informações sobre associações fora de linha, consulte [fontes de dados e associações & #40; SSAS Multidimensional & #41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
