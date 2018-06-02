---
title: Elemento DeleteWithDescendants (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a646a910443055b3fbfb892743493d86e2ba370e
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34574798"
---
# <a name="deletewithdescendants-element-xmla"></a>Elemento DeleteWithDescendants (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Indica se os descendentes de membros de atributo também são excluídos pelo comando pai [Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Drop>  
   ...  
   <DeleteWithDescendants>...</DeleteWithDescendants>  
   ...  
</Drop>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Booliano|  
|Valor padrão|Falso|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O elemento **DeleteWithDescendants** determina se o comando **Drop** não deve apenas excluir os membros de atributo identificados pelo elemento [Where](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md) , mas também que os descendentes daqueles membros de atributo devem ser descartados.  
  
> [!NOTE]  
>  Esse elemento só se aplica a membros de atributos nas hierarquias pai-filho.  
  
 Para obter mais informações sobre a exclusão e atualização de membros de atributo, consulte [Inserindo, atualizando e descartando membros &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md).  
  
## <a name="see-also"></a>Confira também
 [Propriedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
