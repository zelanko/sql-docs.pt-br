---
title: Chave de elemento (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Key Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Key
- urn:schemas-microsoft-com:xml-analysis#Key
- microsoft.xml.analysis.key
helpviewer_keywords:
- Key element
ms.assetid: 09d3cd48-49f7-4b58-b8bb-ca75b81bb02f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f1532db273c83f16678d278f068befefcd8df4b4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48101276"
---
# <a name="key-element-xmla"></a>Elemento Key (XMLA)
  Contém um valor de chave de membro para um membro de atributo.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Keys>  
   ...  
   <Key>...</Key>  
   ...  
</Keys>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Any (qualquer)|  
|Valor padrão|None|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Chaves](keys-element-xmla.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O tipo de dados usado por este elemento deve corresponder ao tipo de dados da coluna de chave adequada do atributo especificado. Se os elementos `Key` não forem especificados para um elemento pai `Attribute`, os elementos `AttributeName` e `Name` especificados no elemento pai `Attribute` serão usados para identificar o membro de atributo a ser modificado.  
  
## <a name="see-also"></a>Consulte também  
 [Atributo do elemento &#40;XMLA&#41;](attribute-element-xmla.md)   
 [Elemento AttributeName &#40;XMLA&#41;](name-element-xmla.md)   
 [Elemento drop &#40;XMLA&#41;](../xml-elements-commands/drop-element-xmla.md)   
 [Inserir o elemento &#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [Elemento KeyColumn &#40;ASSL&#41;](../../scripting/objects/column-element-assl.md)   
 [Atualizar o elemento &#40;XMLA&#41;](../xml-elements-commands/update-element-xmla.md)   
 [Em que elemento de &#40;XMLA&#41;](where-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
