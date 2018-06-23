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
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 665626323e435eeed50b73f4d94de4506dba4f19
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008993"
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
|[Descartar](../xml-elements-commands/drop-element-xmla.md), [onde](name-element-xmla.md), [chaves](keys-element-xmla.md)|  
|[Inserir](../xml-elements-commands/insert-element-xmla.md), [atualização](../xml-elements-commands/update-element-xmla.md)|[AttributeName](name-element-xmla.md), [CustomRollup](customrollup-element-xmla.md), [CustomRollupProperties](properties-element-xmla.md), [chaves](keys-element-xmla.md), [nome](name-element-xmla.md), [ SkippedLevels](skippedlevels-element-xmla.md), [traduções](translations-element-xmla.md), [UnaryOperator](unaryoperator-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 O `Attribute` elemento define o membro de atributo que é inserido, atualizado ou excluído, respectivamente, pelo `Insert`, `Update`, ou `Drop` comando. Como esses comandos podem ser operados somente em um membro de atributo por vez, o [atributos](attributes-element-xmla.md) coleção do `Insert`, `Update`, e `Drop` comandos podem conter apenas um `Attribute` elemento. No entanto, a coleção `Attributes` do elemento `Where` para os comandos `Drop` e `Update` pode conter mais de um elemento `Attribute`, de modo que os atributos podem ser filtrados para serem descartados ou atualizados em uma dimensão habilitada para gravação.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)   
 [Dimensões habilitadas para gravação](../../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  