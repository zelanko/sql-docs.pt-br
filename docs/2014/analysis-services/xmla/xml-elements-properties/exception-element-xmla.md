---
title: Elemento Exception (XMLA) | Microsoft Docs
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
- Exception Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Exception
- urn:schemas-microsoft-com:xml-analysis#Exception
- microsoft.xml.analysis.exception
helpviewer_keywords:
- Exception element
ms.assetid: 0be4cc2f-c03e-490a-a6f7-8b1ede5d09ba
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 33af06aa3243b0860bca6d9ae8ff15595ae1ad4f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37156807"
---
# <a name="exception-element-xmla"></a>Elemento Exception (XMLA)
  Indica se uma exceção foi retornada de uma [Discover](../xml-elements-methods-discover.md) ou [Execute](../xml-elements-methods-execute.md) chamada de método.  
  
 **Namespace** http://schemas.microsoft.com/analysisservices/2003/exception  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<root>  
   ...  
   <Exception />  
   ...  
</root>  
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
|Elementos pai|[root](root-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Se ocorrer um erro durante a execução de uma chamada do método `Discover` ou de um único comando XMLA em uma chamada do método `Execute` que impede a conclusão do método ou comando, o elemento `root` do método ou comando em questão conterá um elemento `Exception` e um elemento `Messages`. O elemento `Exception` indica que ocorreu um erro que impediu a execução com êxito do método ou comando e o elemento `Messages` contém a lista de erros ou mensagens de aviso relacionados ao erro.  
  
## <a name="see-also"></a>Consulte também  
 [Mensagens de elemento &#40;XMLA&#41;](messages-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
