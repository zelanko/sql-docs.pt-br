---
title: Mensagem elemento (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Message Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.message
- http://schemas.microsoft.com/analysisservices/2003/engine#Message
- urn:schemas-microsoft-com:xml-analysis#Message
helpviewer_keywords:
- Message element
ms.assetid: 028911e2-9779-43b1-824d-6d7fb2295885
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 513b0b4be9666d667bd33221552fd792e92e3790
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="message-element-xmla"></a>Elemento Message (XMLA)
  Contém uma mensagem retornada de uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] por um [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) ou [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) chamada de método.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Messages>  
   ...  
   <Message>  
      <Error>...</Error>  
      <!-- or -->  
      <Warning>...</Warning>  
   </Message>  
   ...  
</Messages>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Mensagens](../../../analysis-services/xmla/xml-elements-properties/messages-element-xmla.md)|  
|Elementos filho|[Erro](../../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md), [aviso](../../../analysis-services/xmla/xml-elements-properties/warning-element-xmla.md)|  
  
## <a name="remarks"></a>Comentários  
 Esse elemento é usado em casos nos quais uma chamada de método **Discover** ou um único comando XMLA em uma chamada de método **Execute** é concluída com êxito, mas com erros ou avisos. Nesses casos, um **mensagens** elemento é adicionado ao elemento raiz depois de todos os outros elementos, que por sua vez, contém um ou mais **mensagem** elementos. Cada elemento **Message** representa uma única mensagem, um erro ou um aviso, retornado pela instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

