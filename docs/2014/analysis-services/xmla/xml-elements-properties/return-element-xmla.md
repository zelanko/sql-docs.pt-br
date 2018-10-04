---
title: Elemento Return (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9484532d235d923dae8b28ab42bd7e4af4523346
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48217526"
---
# <a name="return-element-xmla"></a>Elemento return (XMLA)
  Contém informações retornadas por uma [DiscoverResponse](../xml-elements-objects-discoverresponse.md) elemento em resposta a um [Discover](../xml-elements-methods-discover.md) chamada de método ou uma [ExecuteResponse](../xml-elements-objects-executeresponse.md) elemento em resposta a uma [Execute](../xml-elements-methods-execute.md) chamada de método.  
  
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
|Comprimento e tipo de dados|None|  
|Valor padrão|None|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[DiscoverResponse](../xml-elements-objects-discoverresponse.md), [ExecuteResponse](../xml-elements-objects-executeresponse.md)|  
|Ancestral:[DiscoverResponse](../xml-elements-objects-discoverresponse.md)|Filho: <br />                        [root](root-element-xmla.md)|  
|Ancestral: <br />                        [ExecuteResponse](../xml-elements-objects-executeresponse.md)|Filho: [raiz](root-element-xmla.md) ou [resultados](results-element-xmla.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento `return` contém os dados retornados pelos métodos `Discover` e `Execute`. Normalmente, o elemento `return` contém um único elemento `root` que contém os dados retornados pela chamada bem-sucedida do método `Discover` ou `Execute` ou uma exceção XMLA (XML for Analysis) retornada por uma chamada de método malsucedida. Se o método `Execute` contiver um comando `Batch` que executa várias operações, o elemento `return` conterá um elemento `results` que, por sua vez, conterá um elemento `root` para cada comando executado com êxito ou não pelo comando `Batch`.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
