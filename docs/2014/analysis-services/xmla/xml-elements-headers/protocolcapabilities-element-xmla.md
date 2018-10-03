---
title: Elemento ProtocolCapabilities (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ProtocolCapabilities Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.protocolcapabilities
- http://schemas.microsoft.com/analysisservices/2003/engine#ProtocolCapabilities
- urn:schemas-microsoft-com:xml-analysis#ProtocolCapabilities
helpviewer_keywords:
- ProtocolCapabilities element
ms.assetid: f923896a-3f32-46a3-9543-388c30b3465d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 12e4cac0c9846582c40213048e71c7f3793ff736
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219036"
---
# <a name="protocolcapabilities-element-xmla"></a>Elemento ProtocolCapabilities (XMLA)
  Usa o cabeçalho SOAP em uma mensagem de solicitação SOAP para identificar os recursos de protocolo entre uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e um aplicativo cliente.  
  
 **namespace** http://schemas.microsoft.com/analysisservices/2003/engine  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
   <soap:Header>  
      ...  
      <ProtocolCapabilities xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
         <Capability>...</Capability>  
      </ProtocolCapabilities>  
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
|Comprimento e tipo de dados|None|  
|Valor padrão|None|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|None|  
|Elementos filho|[Recurso](../xml-elements-properties/capability-element-xmla.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento `ProtocolCapabilities` permite que os aplicativos cliente negociem os recursos de protocolo com uma instância [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], como o suporte à compactação ou XML binário, a qualquer momento. A negociação dos recursos de protocolo envolve as seguintes etapas:  
  
1.  O aplicativo cliente identifica seu recurso de protocolo enviando uma solicitação SOAP que inclui o `ProtocolCapabilities` elemento como parte do cabeçalho SOAP.  
  
2.  A instância [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] recebe e processa a solicitação SOAP.  
  
3.  Se a instância [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] tiver o mesmo recurso de protocolo que foi solicitado, a instância enviará uma resposta SOAP que inclui o mesmo elemento `ProtocolCapabilities` enviado na solicitação SOAP e o protocolo terá sido negociado com êxito. Caso contrário, os recursos de protocolo não serão negociadas com êxito e a instância retornará uma falha SOAP.  
  
 Após a negociação bem-sucedida dos recursos de protocolo, quanto tempo o aplicativo cliente e o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] um protocolo específico de uso de instância depende se a sessão é explícita ou implícita:  
  
-   Uma sessão explícita é aquela criada usando o [BeginSession](session-element-xmla.md) elemento de cabeçalho. Para uma sessão explícita, o protocolo negociado é usado até que o aplicativo cliente envia uma nova `ProtocolCapabilities` elemento ou o término da sessão.  
  
-   Uma sessão implícita é aquela que foi criada por uma instância [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e não foi explicitamente especificada pelo aplicativo cliente no momento do envio da solicitação SOAP. Em uma sessão implícita, o protocolo negociado só é usado até que a solicitação SOAP seja concluída.  
  
 Os recursos de protocolo não precisam ser negociados explicitamente. Ou seja, um aplicativo cliente não precisa incluir um `ProtocolCapabilities` elemento como parte da solicitação SOAP. Caso uma solicitação SOAP não inclua um elemento `ProtocolCapabilities`, a instância [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] responderá usando o mesmo formato usado na solicitação SOAP.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando conexões e sessões &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Cabeçalhos &#40;XMLA&#41;](xml-elements-headers.md)  
  
  
