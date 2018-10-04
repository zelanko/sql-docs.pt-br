---
title: Mensagens de elemento (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Messages Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Messages
- microsoft.xml.analysis.messages
- urn:schemas-microsoft-com:xml-analysis#Messages
helpviewer_keywords:
- Messages element
ms.assetid: 719d15ff-f18b-4c56-80ba-a9114c0b7d8a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4bb3d7e97332909864a7762291d39dbb4802b07e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48103096"
---
# <a name="messages-element-xmla"></a>Elemento Messages (XMLA)
  Contém uma coleção de elementos [Message](message-element-xmla.md) retounados de uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] pela chamada de um método [Discover](../xml-elements-methods-discover.md) ou [Execute](../xml-elements-methods-execute.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Resultset>  
   <Messages>  
      <Message>  
   </Messages>  
</Resultset>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|None|  
|Valor padrão|None|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Conjunto de resultados](../xml-data-types/resultset-data-type-xmla.md)|  
|Elementos filho|[Mensagem](message-element-xmla.md)|  
  
## <a name="remarks"></a>Comentários  
 Esse elemento é usado em casos nos quais uma chamada de método `Discover` ou um único comando XMLA em uma chamada de método `Execute` é concluída com êxito, mas com erros ou avisos. Nesses casos, uma `Messages` elemento é adicionado para o [raiz](root-element-xmla.md) elemento após todos os outros elementos, que por sua vez, contém um ou mais `Message` elementos. Cada `Message` elemento representa uma única mensagem, um erro ou um aviso, retornado pela [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
