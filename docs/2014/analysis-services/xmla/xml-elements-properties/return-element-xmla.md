---
title: Elemento Return (XMLA) | Microsoft Docs
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
- return Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.return
- http://schemas.microsoft.com/analysisservices/2003/engine#return
- urn:schemas-microsoft-com:xml-analysis#return
helpviewer_keywords:
- return element
ms.assetid: 3cfe8b74-fec3-4987-a74a-5f731444e024
caps.latest.revision: 14
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 1a4468ce3d4b14ff9cd9db7c9373083aad75d3eb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36005710"
---
# <a name="return-element-xmla"></a>Elemento return (XMLA)
  Contém informações retornadas por uma [DiscoverResponse](../xml-elements-objects-discoverresponse.md) elemento em resposta a um [Discover](../xml-elements-methods-discover.md) chamada de método ou um [ExecuteResponse](../xml-elements-objects-executeresponse.md) elemento em resposta a um [Execute](../xml-elements-methods-execute.md) chamada de método.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DiscoverResponse> <!-- or ExecuteResponse -->  
   <return>  
      <root>...</root>  
      <!-- or -->  
      <results>...</results> <!-- ExecuteResponse only -->  
   </return>  
</DiscoverResponse>  
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
|Elementos pai|[DiscoverResponse](../xml-elements-objects-discoverresponse.md), [ExecuteResponse](../xml-elements-objects-executeresponse.md)|  
|Ancestral:[DiscoverResponse](../xml-elements-objects-discoverresponse.md)|Filho: <br />                        [root](root-element-xmla.md)|  
|Ancestral: <br />                        [ExecuteResponse](../xml-elements-objects-executeresponse.md)|Filho: [raiz](root-element-xmla.md) ou [resultados](results-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento `return` contém os dados retornados pelos métodos `Discover` e `Execute`. Normalmente, o elemento `return` contém um único elemento `root` que contém os dados retornados pela chamada bem-sucedida do método `Discover` ou `Execute` ou uma exceção XMLA (XML for Analysis) retornada por uma chamada de método malsucedida. Se o método `Execute` contiver um comando `Batch` que executa várias operações, o elemento `return` conterá um elemento `results` que, por sua vez, conterá um elemento `root` para cada comando executado com êxito ou não pelo comando `Batch`.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  