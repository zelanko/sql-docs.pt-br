---
title: Chave de elemento (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bea00c5b5fdff010d667db19ef3af28284ce3ed9
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34575778"
---
# <a name="key-element-xmla"></a>Elemento Key (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
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
|Elementos pai|[Chaves](../../../analysis-services/xmla/xml-elements-properties/keys-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O tipo de dados usado por este elemento deve corresponder ao tipo de dados da coluna de chave adequada do atributo especificado. Se os elementos **Key** não forem especificados para um elemento pai **Attribute** , os elementos **AttributeName** e **Name** especificados no elemento pai **Attribute** serão usados para identificar o membro de atributo a ser modificado.  
  
## <a name="see-also"></a>Confira também
 [Atributo de elemento &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)   
 [Elemento AttributeName &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/attributename-element-xmla.md)   
 [Elemento drop &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)   
 [Elemento Insert &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Elemento KeyColumn &#40;ASSL&#41;](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)   
 [Elemento Update &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [Onde elemento &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
