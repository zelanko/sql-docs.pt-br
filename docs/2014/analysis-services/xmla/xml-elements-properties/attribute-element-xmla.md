---
title: Atributo de elemento (XMLA) | Microsoft Docs
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
- Attribute Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Attribute
- microsoft.xml.analysis.attribute
- urn:schemas-microsoft-com:xml-analysis#Attribute
helpviewer_keywords:
- Attribute element
ms.assetid: 0df9cf44-dc5f-4234-8a5a-daac8aabc0d6
caps.latest.revision: 17
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 262114f7bbd9200bfab3a74bb14e8cea08400f5d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37185113"
---
# <a name="attribute-element-xmla"></a>Elemento Attribute (XMLA)
  Define ou filtra um membro em um atributo no qual um pai [inserir](../xml-elements-commands/insert-element-xmla.md), [atualização](../xml-elements-commands/update-element-xmla.md), ou [Drop](../xml-elements-commands/drop-element-xmla.md) comando executa.  
  
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Atributos](attributes-element-xmla.md)|  
  
 **Elementos filho**  
  
|||  
|-|-|  
|**Ancestral ou pai**|**Elemento filho**|  
|[Drop](../xml-elements-commands/drop-element-xmla.md), [onde](name-element-xmla.md), [chaves](keys-element-xmla.md)|  
|[Inserir](../xml-elements-commands/insert-element-xmla.md), [atualização](../xml-elements-commands/update-element-xmla.md)|[AttributeName](name-element-xmla.md), [CustomRollup](customrollup-element-xmla.md), [CustomRollupProperties](properties-element-xmla.md), [chaves](keys-element-xmla.md), [nome](name-element-xmla.md), [ SkippedLevels](skippedlevels-element-xmla.md), [traduções](translations-element-xmla.md), [UnaryOperator](unaryoperator-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 O `Attribute` elemento define o membro de atributo que é inserido, atualizada ou excluída, respectivamente, pelo `Insert`, `Update`, ou `Drop` comando. Como esses comandos podem ser operados somente em um membro de atributo por vez, o [atributos](attributes-element-xmla.md) coleção da `Insert`, `Update`, e `Drop` comandos podem conter apenas um `Attribute` elemento. No entanto, a coleção `Attributes` do elemento `Where` para os comandos `Drop` e `Update` pode conter mais de um elemento `Attribute`, de modo que os atributos podem ser filtrados para serem descartados ou atualizados em uma dimensão habilitada para gravação.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)   
 [Dimensões habilitadas para gravação](../../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
