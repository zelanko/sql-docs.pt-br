---
title: Atributo de elemento (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Attribute Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Attribute
- microsoft.xml.analysis.attribute
- urn:schemas-microsoft-com:xml-analysis#Attribute
helpviewer_keywords:
- Attribute element
ms.assetid: 0df9cf44-dc5f-4234-8a5a-daac8aabc0d6
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2ea4bdfb2ca301a3919be6786c383a33d4561727
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="attribute-element-xmla"></a>Elemento Attribute (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Define ou filtra um membro em um atributo no qual um comando pai [Insert](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md), [Update](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)ou [Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md) é executado.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Attributes>  
   ...  
   <Attribute>  
      <AttributeName>...</AttributeName>  
      <Keys>...</Keys>  
      <!-- The following elements are included only for attributes contained in the Attributes element of a parent Insert or Update command -->  
      <Name>...</Name>  
      <Translations>...</Translations>  
      <CustomRollup>...</CustomRollup>  
      <CustomRollupProperties>...</CustomRollupProperties>  
      <UnaryOperator>...</UnaryOperator>  
      <SkippedLevels>...</SkippedLevels>  
   </Attribute>  
   ...  
</Attributes>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Atributos](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md)|  
|Elementos filho|Veja a tabela abaixo.|  
  
|Ancestral ou pai|Elemento filho|  
|------------------------|-------------------|  
|[Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md), [Where](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md)|[AttributeName](../../../analysis-services/xmla/xml-elements-properties/attributename-element-xmla.md), [Keys](../../../analysis-services/xmla/xml-elements-properties/keys-element-xmla.md)|  
|[Insert](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md), [Update](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|[AttributeName](../../../analysis-services/xmla/xml-elements-properties/attributename-element-xmla.md), [CustomRollup](../../../analysis-services/xmla/xml-elements-properties/customrollup-element-xmla.md), [CustomRollupProperties](../../../analysis-services/xmla/xml-elements-properties/customrollupproperties-element-xmla.md), [Keys](../../../analysis-services/xmla/xml-elements-properties/keys-element-xmla.md), [Name](../../../analysis-services/xmla/xml-elements-properties/name-element-xmla.md), [SkippedLevels](../../../analysis-services/xmla/xml-elements-properties/skippedlevels-element-xmla.md), [Translations](../../../analysis-services/xmla/xml-elements-properties/translations-element-xmla.md), [UnaryOperator](../../../analysis-services/xmla/xml-elements-properties/unaryoperator-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento **Attribute** define o membro de atributo que é inserido, atualizado ou excluído, respectivamente, pelo comando **Insert**, **Update**ou **Drop** . Como esses comandos podem ser operados somente em um membro de atributo por vez, o [atributos](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md) coleção do **inserir**, **atualização**, e **Drop**comandos podem conter apenas um **atributo** elemento. No entanto, a coleção **Attributes** do elemento **Where** para os comandos **Drop** e **Update** pode conter mais de um elemento **Attribute** , de modo que os atributos podem ser filtrados para serem descartados ou atualizados em uma dimensão habilitada para gravação.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)   
 [Dimensões habilitadas para gravação](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
