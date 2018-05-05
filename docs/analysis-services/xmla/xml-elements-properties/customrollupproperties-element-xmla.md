---
title: Elemento CustomRollupProperties (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- CustomRollupProperties Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.customrollupproperties
- urn:schemas-microsoft-com:xml-analysis#CustomRollupProperties
- http://schemas.microsoft.com/analysisservices/2003/engine#CustomRollupProperties
helpviewer_keywords:
- CustomRollupProperties element
ms.assetid: 4abf0129-e529-4355-b8d5-6f4e6a88e796
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 696b444efaf8f6eb71e365854b0978c610eb738e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="customrollupproperties-element-xmla"></a>Elemento CustomRollupProperties (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contém as propriedades de acúmulo personalizado para um membro de atributo representado pelo elemento pai [Attribute](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Attribute>  
   ...  
   <CustomRollupProperties>...</CustomRollupProperties>  
   ...  
</Attribute>  
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
|Elementos pai|[Atributo](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 O elemento **CustomRollupProperties** contém uma linguagem MDX que define as propriedades de acúmulo personalizado do membro de atributo definido pelo elemento pai **Attribute** .  
  
 Para obter mais informações sobre expressões MDX, consulte [expressões & #40; MDX & #41; ](../../../mdx/expressions-mdx.md).  
  
## <a name="see-also"></a>Consulte também  
 [Inserir o elemento & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Atualizar o elemento & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
