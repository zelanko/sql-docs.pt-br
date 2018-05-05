---
title: Mensagens de elemento (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Messages Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Messages
- microsoft.xml.analysis.messages
- urn:schemas-microsoft-com:xml-analysis#Messages
helpviewer_keywords:
- Messages element
ms.assetid: 719d15ff-f18b-4c56-80ba-a9114c0b7d8a
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 5e8cf8540e01b22968abe0c124fe4c4b5172a8ba
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="messages-element-xmla"></a>Elemento Messages (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contém uma coleção de elementos [Message](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md) retounados de uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] pela chamada de um método [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) ou [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Resultset>  
   <Messages>  
      <Message>  
   </Messages>  
</Resultset>  
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
|Elementos pai|[Conjunto de resultados](../../../analysis-services/xmla/xml-data-types/resultset-data-type-xmla.md)|  
|Elementos filho|[Mensagem](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 Esse elemento é usado em casos nos quais uma chamada de método **Discover** ou um único comando XMLA em uma chamada de método **Execute** é concluída com êxito, mas com erros ou avisos. Em tais casos, um elemento **Messages** é adicionado ao elemento [raiz](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) depois de todos os elementos, que, por sua vez, contêm um ou mais elementos **Message** . Cada elemento **Message** representa uma única mensagem, um erro ou um aviso, retornado pela instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
