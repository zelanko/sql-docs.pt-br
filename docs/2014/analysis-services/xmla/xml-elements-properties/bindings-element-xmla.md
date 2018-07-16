---
title: Elemento Bindings (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Bindings Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.bindings
- urn:schemas-microsoft-com:xml-analysis#Bindings
- http://schemas.microsoft.com/analysisservices/2003/engine#Bindings
helpviewer_keywords:
- Bindings element
ms.assetid: caa34cab-f61f-4f39-b800-af1601714daa
caps.latest.revision: 10
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2ee02beeb04987680cf9cf516bc6f25e66287b7b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37302686"
---
# <a name="bindings-element-xmla"></a>Elemento Bindings (XMLA)
  Contém uma coleção de elementos [Binding](binding-element-xmla.md) para o elemento pai [Batch](../xml-elements-commands/batch-element-xmla.md) ou [Process](../xml-elements-commands/process-element-xmla.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Batch> <!-- or Process>  
...  
   <Bindings>  
      <Binding>...</Binding>  
   </Bindings>  
...  
</Alter>  
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
|Elementos pai|[Batch](../xml-elements-commands/batch-element-xmla.md), [Process](../xml-elements-commands/process-element-xmla.md)|  
|Elementos filho|[Associação](binding-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
