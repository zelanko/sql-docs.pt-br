---
title: Nome de elemento (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 422bd152e82a471ce0f130a26aaa12a56026419a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48127896"
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
|Valor padrão|None|  
|Ancestral ou pai:|Cardinalidade|  
|[Atributo](attribute-element-xmla.md)|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
|[Tradução](translation-element-xmla.md)|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Atributo](attribute-element-xmla.md), [tradução](translation-element-xmla.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 Para os elementos `Attribute`, o elemento `Name` contém o nome do membro do atributo a ser inserido ou atualizado, respectivamente, durante o `Insert` ou o comando `Update`.  
  
 Para os elementos `Translation`, o elemento `Name` contém a legenda do membro do atributo, no idioma especificado pelo elemento `Language` do objeto pai `Translation`. Se o elemento `Name` não for especificado ou contiver uma cadeia de caracteres vazia, será usado o valor do elemento `Name` do elemento `Attribute` que contém o elemento `Translation`.  
  
## <a name="see-also"></a>Consulte também  
 [Inserir o elemento &#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [Elemento de linguagem &#40;XMLA&#41;](language-element-xmla.md)   
 [Atualizar o elemento &#40;XMLA&#41;](../xml-elements-commands/update-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
