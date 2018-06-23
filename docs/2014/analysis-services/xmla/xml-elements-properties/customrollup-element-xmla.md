---
title: Elemento CustomRollup (XMLA) | Microsoft Docs
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
- CustomRollup Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#CustomRollup
- http://schemas.microsoft.com/analysisservices/2003/engine#CustomRollup
- microsoft.xml.analysis.customrollup
helpviewer_keywords:
- CustomRollup element
ms.assetid: b266ac8b-1ae7-461c-9127-3c5642f829f5
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 715aca3e7bb35eb082a9e6fecc286aaf30ff3b71
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121561"
---
# <a name="customrollup-element-xmla"></a>Elemento CustomRollup (XMLA)
  Contém a fórmula de acúmulo personalizado para um membro de atributo representado pelo pai [atributo](attribute-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Attribute>  
   ...  
   <CustomRollup>...</CustomRollup>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Atributo](attribute-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O elemento `CustomRollup` contém uma linguagem MDX que define o comportamento de acúmulo do membro de atributo definido pelo elemento pai `Attribute`.  
  
 Para obter mais informações sobre expressões MDX, consulte [expressões &#40;MDX&#41;](/sql/mdx/expressions-mdx).  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Insert &#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [Elemento Update &#40;XMLA&#41;](../xml-elements-commands/update-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
