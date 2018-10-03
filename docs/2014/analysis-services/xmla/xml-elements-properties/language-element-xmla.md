---
title: Elemento Language (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Language Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Language
- microsoft.xml.analysis.language
- http://schemas.microsoft.com/analysisservices/2003/engine#Language
helpviewer_keywords:
- Language element
ms.assetid: cd998202-e43f-4c6c-8727-a15a76a520ea
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f55255a0f57c92d0a8975b18bcd5f4810ca95d88
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48116217"
---
# <a name="language-element-xmla"></a>Elemento Language (XMLA)
  Contém o identificador de localidade (LCID) para o pai [tradução](translation-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Translation>  
   ...  
   <Language>...</Language>  
   ...  
</Translation>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Integer|  
|Valor padrão|None|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Tradução](translation-element-xmla.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O elemento `Language` especifica o LCID usado pelo elemento pai `Translation` para atribuir o elemento `Name` do elemento pai `Translation` a um membro de atributo, para o idioma especificado, durante um comando `Insert` ou `Update`.  
  
## <a name="see-also"></a>Consulte também  
 [Inserir o elemento &#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [Nomeie o elemento &#40;XMLA&#41;](name-element-xmla.md)   
 [Atualizar o elemento &#40;XMLA&#41;](../xml-elements-commands/update-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
