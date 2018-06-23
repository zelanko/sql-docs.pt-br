---
title: Elemento Restrictions (XMLA) | Microsoft Docs
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
- Restrictions Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Restrictions
- http://schemas.microsoft.com/analysisservices/2003/engine#Restrictions
- microsoft.xml.analysis.restrictions
helpviewer_keywords:
- Restrictions element
ms.assetid: e745ce13-b468-4372-a6f0-0da3d772dda3
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: a096ea973d6b8ba900c3b1d890f49ad019d8e93f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121562"
---
# <a name="restrictions-element-xmla"></a>Elemento Restrictions (XMLA)
  Contém colunas de restrição e dados usados pelo [Discover](../xml-elements-methods-discover.md) método.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Discover>  
...  
   <Restrictions>  
      <RestrictionList>...</RestrictionList>  
   </Restrictions>  
...  
</Discover>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Descobrir](../xml-elements-methods-discover.md)|  
|Elementos filho|[RestrictionList](restrictionlist-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento `Restrictions` representa colunas de restrição e dados usados para restringir a informações recuperadas pelo método `Discover`.  
  
## <a name="example"></a>Exemplo  
  
```  
<Discover xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <RequestType>DISCOVER_PROPERTIES</RequestType>  
   <Restrictions>  
      <RestrictionList xmlns="urn:schemas-microsoft-com:xml-analysis">  
         <PropertyName>Catalog</PropertyName>  
      </RestrictionList>  
   </Restrictions>  
   <Properties />  
</Discover>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  