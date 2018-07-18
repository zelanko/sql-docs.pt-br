---
title: Elemento RestrictionList (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c802b20b0e2d6212f68fa4dc43c35426ff377957
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37994778"
---
# <a name="restrictionlist-element-xmla"></a>Elemento RestrictionList (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contém uma coleção de colunas de restrição e valores usados pelo método [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Restrictions>  
   <RestrictionList>  
      <!-- Zero or more restriction columns and values -->  
   </RestrictionList>  
</Restrictions>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Restrições](../../../analysis-services/xmla/xml-elements-properties/restrictions-element-xmla.md)|  
|Elementos filho|Colunas e valores de restrição (consulte os Comentários).|  
  
## <a name="remarks"></a>Remarks  
 O elemento **RestrictionList** contém uma coleção de colunas de restrição na qual os dados retornados pelo método **Discover** podem ser filtrados. Cada coluna de restrição no elemento **RestrictionList** está definida por um elemento XML separado. O valor da coluna de restrição são os dados contidos pelo elemento XML e o nome da coluna de restrição corresponde ao nome do elemento XML.  
  
## <a name="see-also"></a>Confira também
 [Propriedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
