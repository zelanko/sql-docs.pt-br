---
title: Elemento ProtocolCapabilities (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 85ddeb22fac03e5ae7f66521ac3ca8a46e210fe7
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38021191"
---
# <a name="protocolcapabilities-element-xmla"></a>Elemento ProtocolCapabilities (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Usa o cabeçalho SOAP em uma mensagem de solicitação SOAP para identificar os recursos de protocolo entre uma instância do Analysis Services e um aplicativo cliente.  
  
 **Namespace** `http://schemas.microsoft.com/analysisservices/2003/engine`  
  
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
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhum|  
|Elementos filho|[Recurso](../../../analysis-services/xmla/xml-elements-properties/capability-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 O **ProtocolCapabilities** elemento permite que os aplicativos cliente negociem os recursos de protocolo, como suporte à compactação ou XML binário, com um [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância a qualquer momento. A negociação dos recursos de protocolo envolve as seguintes etapas:  
  
1.  O aplicativo cliente identifica seu recurso de protocolo enviando uma solicitação SOAP que inclua o elemento **ProtocolCapabilities** como parte do cabeçalho SOAP.  
  
2.  A instância [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] recebe e processa a solicitação SOAP.  
  
3.  Se o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância tem a mesma funcionalidade de protocolo que foi solicitado, a instância enviará uma resposta SOAP que inclui o mesmo **ProtocolCapabilities** elemento enviado na solicitação SOAP e o protocolo foi negociado com êxito. Caso contrário, os recursos de protocolo não serão negociadas com êxito e a instância retornará uma falha SOAP.  
  
 Após a negociação bem-sucedida dos recursos de protocolo, quanto tempo o aplicativo cliente e o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] um protocolo específico de uso de instância depende se a sessão é explícita ou implícita:  
  
-   Uma sessão explícita é aquela criada usando o [BeginSession](../../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md) elemento de cabeçalho. Em uma sessão explícita, o protocolo negociado é usado até que o aplicativo cliente envie um novo elemento **ProtocolCapabilities** ou até o término da sessão.  
  
-   Uma sessão implícita é aquela que foi criada por uma instância [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e não foi explicitamente especificada pelo aplicativo cliente no momento do envio da solicitação SOAP. Em uma sessão implícita, o protocolo negociado só é usado até que a solicitação SOAP seja concluída.  
  
 Os recursos de protocolo não precisam ser negociados explicitamente. Ou seja, um aplicativo cliente não precisa incluir um elemento **ProtocolCapabilities** como parte da solicitação SOAP. Se uma solicitação SOAP não inclua uma **ProtocolCapabilities** elemento, o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância responde usando o mesmo formato usado na solicitação SOAP.  
  
## <a name="see-also"></a>Confira também
 [Gerenciando conexões e sessões &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Cabeçalhos &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)  
  
  
