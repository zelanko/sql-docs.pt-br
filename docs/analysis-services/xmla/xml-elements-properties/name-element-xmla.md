---
title: Nome de elemento (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4f19696ae5eea630a6fe879b603b72c4e955b1ac
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="name-element-xmla"></a>Elemento Name (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contém o nome de um membro de atributo para o pai [atributo](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md) ou [tradução](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Attribute> <!-- or Translation -->  
   ...  
   <Name>...</Name>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|Veja a tabela abaixo.|  
  
|Ancestral ou pai|Cardinalidade|  
|------------------------|-----------------|  
|[Atributo](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
|[Tradução](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Atributo](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md), [tradução](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 Para **atributo** elementos, o **nome** elemento contém o nome do membro do atributo a ser inserido ou atualizado durante, respectivamente, o **inserir** ou **Atualização** comando.  
  
 Para **tradução** elementos, o **nome** elemento contém a legenda do membro do atributo, no idioma especificado pelo **idioma** elemento do pai  **Tradução** objeto. Se o **nome** elemento não for especificado ou contiver uma cadeia de caracteres vazia, o valor da **nome** elemento para o **atributo** elemento que contém o  **Tradução** elemento é usado.  
  
## <a name="see-also"></a>Consulte também  
 [Inserir o elemento & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Elemento de linguagem &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/language-element-xmla.md)   
 [Atualizar o elemento & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
