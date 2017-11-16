---
title: Elemento Exception (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Exception Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Exception
- urn:schemas-microsoft-com:xml-analysis#Exception
- microsoft.xml.analysis.exception
helpviewer_keywords:
- Exception element
ms.assetid: 0be4cc2f-c03e-490a-a6f7-8b1ede5d09ba
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0c83900d85d698c5f9b2c0bdca2c197ab4ce05b1
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="exception-element-xmla"></a>Elemento Exception (XMLA)
  Indica se uma exceção foi retornada de uma [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) ou [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) chamada de método.  
  
 **Namespace**`http://schemas.microsoft.com/analysisservices/2003/exception`  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<root>  
   ...  
   <Exception />  
   ...  
</root>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[raiz](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Se ocorrer um erro durante a execução de uma chamada do método **Discover** ou de um único comando XMLA em uma chamada do método **Execute** que impede a conclusão do método ou comando, o elemento **root** do método ou comando em questão conterá um elemento **Exception** e um elemento **Messages** . O elemento **Exception** indica que ocorreu um erro que impediu a execução com êxito do método ou comando e o elemento **Messages** contém a lista de erros ou mensagens de aviso relacionados ao erro.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Messages &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/messages-element-xmla.md)   
 [Propriedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

