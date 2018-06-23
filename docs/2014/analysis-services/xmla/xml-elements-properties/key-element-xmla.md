---
title: Chave de elemento (XMLA) | Microsoft Docs
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
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: d6ec30e8c55648975294f82a7c927b3815b00471
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006426"
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
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Chaves](keys-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O tipo de dados usado por este elemento deve corresponder ao tipo de dados da coluna de chave adequada do atributo especificado. Se os elementos `Key` não forem especificados para um elemento pai `Attribute`, os elementos `AttributeName` e `Name` especificados no elemento pai `Attribute` serão usados para identificar o membro de atributo a ser modificado.  
  
## <a name="see-also"></a>Consulte também  
 [Atributo de elemento &#40;XMLA&#41;](attribute-element-xmla.md)   
 [Elemento AttributeName &#40;XMLA&#41;](name-element-xmla.md)   
 [Elemento drop &#40;XMLA&#41;](../xml-elements-commands/drop-element-xmla.md)   
 [Elemento Insert &#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [Elemento KeyColumn &#40;ASSL&#41;](../../scripting/objects/column-element-assl.md)   
 [Elemento Update &#40;XMLA&#41;](../xml-elements-commands/update-element-xmla.md)   
 [Onde elemento &#40;XMLA&#41;](where-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  