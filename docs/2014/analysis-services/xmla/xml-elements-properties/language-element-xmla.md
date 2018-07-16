---
title: Elemento Language (XMLA) | Microsoft Docs
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
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d247e81c19c3394ac46274ba775c1695741e00ff
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37205846"
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
|Valor padrão|Nenhum|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Tradução](translation-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O elemento `Language` especifica o LCID usado pelo elemento pai `Translation` para atribuir o elemento `Name` do elemento pai `Translation` a um membro de atributo, para o idioma especificado, durante um comando `Insert` ou `Update`.  
  
## <a name="see-also"></a>Consulte também  
 [Inserir o elemento &#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [Nomeie o elemento &#40;XMLA&#41;](name-element-xmla.md)   
 [Atualizar o elemento &#40;XMLA&#41;](../xml-elements-commands/update-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
