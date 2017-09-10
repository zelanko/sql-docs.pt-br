---
title: Elemento BeginSession (XMLA) | Microsoft Docs
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
- BeginSession Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#BeginSession
- urn:schemas-microsoft-com:xml-analysis#BeginSession
- microsoft.xml.analysis.beginsession
helpviewer_keywords:
- BeginSession element
ms.assetid: 49873a97-58d7-42a9-ab7f-e045e2856737
caps.latest.revision: 16
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b3ebacd7677aecf7c953d966e3001cbe8f8f7691
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O **BeginSession** elemento de cabeçalho é parte de uma solicitação SOAP enviada a um [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância e inicia explicitamente uma nova sessão na instância. O cabeçalho SOAP retornado pela resposta de SOAP contém um [sessão](../../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md) elemento que identifica a nova sessão. Esse identificador de nova sessão é armazenado e enviado em solicitações SOAP subsequentes usando o **sessão** elemento de cabeçalho.  
  
 Se o **BeginSession** elemento de cabeçalho não é enviado, uma sessão não será iniciada explicitamente. Se uma sessão não for iniciada explicitamente, as transações não poderão ser gerenciadas naquela sessão. Em outras palavras, você não pode usar o seguinte XML para comandos Analysis (XMLA): [BeginTransaction](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md), [CommitTransaction](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md), e [RollbackTransaction](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md). Todos os métodos e comandos XMLA executados em uma sessão iniciada implicitamente são considerados transações atômicas.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento EndSession &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md)   
 [Elemento Session &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md)   
 [Gerenciando conexões e sessões &#40; XMLA &#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Cabeçalhos &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)  
  
  
