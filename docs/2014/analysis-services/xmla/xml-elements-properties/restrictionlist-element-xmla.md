---
title: Elemento RestrictionList (XMLA) | Microsoft Docs
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
- RestrictionList Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#RestrictionList
- microsoft.xml.analysis.restrictionlist
- http://schemas.microsoft.com/analysisservices/2003/engine#RestrictionList
helpviewer_keywords:
- RestrictionList element
ms.assetid: 2297c005-381e-49a4-a207-826f7f9ea93a
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 081722ea3a5bf001b22f8c193cd5530a37809e15
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116660"
---
# <a name="restrictionlist-element-xmla"></a>Elemento RestrictionList (XMLA)
  Contém uma coleção de colunas de restrição e valores usados pelo método [Discover](../xml-elements-methods-discover.md) .  
  
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
|Elementos pai|[Restrições](restrictions-element-xmla.md)|  
|Elementos filho|Colunas e valores de restrição (consulte os Comentários).|  
  
## <a name="remarks"></a>Remarks  
 O elemento `RestrictionList` contém uma coleção de colunas de restrição na qual os dados retornados pelo método `Discover` podem ser filtrados. Cada coluna de restrição no elemento `RestrictionList` está definida por um elemento XML separado. O valor da coluna de restrição são os dados contidos pelo elemento XML e o nome da coluna de restrição corresponde ao nome do elemento XML.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  