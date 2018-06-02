---
title: Elemento CustomRollup (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 769a07116e60fc080e0d9ea9dd5ad60a8ee53fb5
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34574538"
---
# <a name="customrollup-element-xmla"></a>Elemento CustomRollup (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contém a fórmula de acúmulo personalizado para um membro de atributo representado pelo pai [atributo](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md) elemento.  
  
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
|Elementos pai|[Atributo](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O elemento **CustomRollup** contém uma linguagem MDX que define o comportamento de acúmulo do membro de atributo definido pelo elemento pai **Attribute** .  
  
 Para obter mais informações sobre expressões MDX, consulte [expressões &#40;MDX&#41;](../../../mdx/expressions-mdx.md).  
  
## <a name="see-also"></a>Confira também
 [Elemento Insert &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Elemento Update &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
