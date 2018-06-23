---
title: Nome de elemento (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Name Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Name
- urn:schemas-microsoft-com:xml-analysis#Name
- microsoft.xml.analysis.name
helpviewer_keywords:
- Name element
ms.assetid: cc1a93df-0b1b-4c38-9183-4f11c26fea6a
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: d3ae469cc1a02a02dc2bdb2ff7d6db7f75a46a69
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119392"
---
# <a name="name-element-xmla"></a>Elemento Name (XMLA)
  Contém o nome de um membro de atributo para o pai [atributo](attribute-element-xmla.md) ou [tradução](translation-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Attribute> <!-- or Translation -->  
   ...  
   <Name>...</Name>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|Nenhum|  
|Ancestral ou pai:|Cardinalidade|  
|[Atributo](attribute-element-xmla.md)|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
|[Tradução](translation-element-xmla.md)|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Atributo](attribute-element-xmla.md), [tradução](translation-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Para os elementos `Attribute`, o elemento `Name` contém o nome do membro do atributo a ser inserido ou atualizado, respectivamente, durante o `Insert` ou o comando `Update`.  
  
 Para os elementos `Translation`, o elemento `Name` contém a legenda do membro do atributo, no idioma especificado pelo elemento `Language` do objeto pai `Translation`. Se o elemento `Name` não for especificado ou contiver uma cadeia de caracteres vazia, será usado o valor do elemento `Name` do elemento `Attribute` que contém o elemento `Translation`.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Insert &#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [Elemento de linguagem &#40;XMLA&#41;](language-element-xmla.md)   
 [Elemento Update &#40;XMLA&#41;](../xml-elements-commands/update-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  