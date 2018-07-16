---
title: Elemento BeginSession (XMLA) | Microsoft Docs
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
- BeginSession Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#BeginSession
- urn:schemas-microsoft-com:xml-analysis#BeginSession
- microsoft.xml.analysis.beginsession
helpviewer_keywords:
- BeginSession element
ms.assetid: 49873a97-58d7-42a9-ab7f-e045e2856737
caps.latest.revision: 16
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cf272ae8221b66f7ac8390fab900d22d6b8aaf87
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37285822"
---
# <a name="beginsession-element-xmla"></a>Elemento BeginSession (XMLA)
  Usa um cabeçalho SOAP em uma mensagem de solicitação SOAP para iniciar uma nova sessão em uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 **Namespace** urn:schemas-microsoft-com:xml-analysis  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
   <soap:Header>  
      ...  
      <BeginSession  
         xmlns="urn:schemas-microsoft-com:xml-analysis" />  
      ...  
   </soap:Header>  
   <soap:Body>  
      ...  
   </soap:Body>  
</soap:Envelope>  
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
|Elementos pai|Nenhum|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O elemento do cabeçalho `BeginSession` faz parte de uma solicitação SOAP enviada a uma instância de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e inicia explicitamente uma nova sessão na instância. O cabeçalho SOAP retornado pela resposta de SOAP contém um [sessão](session-element-xmla.md) elemento que identifica a nova sessão. Este identificador de nova sessão é armazenado e enviado em solicitações SOAP subsequentes que usam o elemento de cabeçalho `Session`.  
  
 Se o elemento de cabeçalho `BeginSession` não for enviado, uma sessão não será iniciada explicitamente. Se uma sessão não for iniciada explicitamente, as transações não poderão ser gerenciadas naquela sessão. Em outras palavras, é possível usar o XML a seguir para comandos Analysis (XMLA): [BeginTransaction](../xml-elements-commands/begintransaction-element-xmla.md), [CommitTransaction](../xml-elements-commands/committransaction-element-xmla.md), e [RollbackTransaction](../xml-elements-commands/rollbacktransaction-element-xmla.md). Todos os métodos e comandos XMLA executados em uma sessão iniciada implicitamente são considerados transações atômicas.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento EndSession &#40;XMLA&#41;](endsession-element-xmla.md)   
 [Elemento Session &#40;XMLA&#41;](session-element-xmla.md)   
 [Gerenciando conexões e sessões &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Cabeçalhos &#40;XMLA&#41;](xml-elements-headers.md)  
  
  
