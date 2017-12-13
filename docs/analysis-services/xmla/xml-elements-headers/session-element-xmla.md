---
title: Elemento Session (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Session Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.session
- http://schemas.microsoft.com/analysisservices/2003/engine#Session
- urn:schemas-microsoft-com:xml-analysis#Session
helpviewer_keywords: Session element
ms.assetid: 884ed090-968e-41d3-97e5-6d12787467da
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1219141676ccdad4060ce4e5b95eb5297863f210
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="session-element-xmla"></a>Elemento Session (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Usa o cabeçalho SOAP em uma mensagem de solicitação SOAP para identificar uma sessão existente explícita em uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 **Namespace** urn:schemas-microsoft-com:xml-analysis  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
   <soap:Header>  
      ...  
      <Session  
         xmlns="urn:schemas-microsoft-com:xml-analysis"  
         SessionId="string" />  
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
|Elementos filho|Nenhum.|  
  
## <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|SessionId|Atributo obrigatório **String** que identifica a sessão a ser usada. O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] usa um GUID (identificador global exclusivo) para identificar uma sessão.|  
  
## <a name="remarks"></a>Comentários  
 O **sessão** elemento de cabeçalho identifica uma sessão existente explicitamente iniciada na [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância. O elemento **Session** faz parte do cabeçalho SOAP nos seguintes tipos de mensagens:  
  
-   Uma resposta SOAP que contém um [BeginSession](../../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md) elemento de cabeçalho SOAP.  
  
-   Uma solicitação SOAP para identificar a sessão na qual executar o [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) ou [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) método.  
  
 Um identificador de sessão não garante que uma sessão permaneça válida. A sessão especificada no elemento **Session** pode expirar. Por exemplo, uma sessão pode expirar se o tempo da sessão atingir seu limite ou se a conexão associada à sessão for interrompida. Se a sessão expirar e não for mais válida, o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] finalizará a sessão e reverterá as transações que estiverem em andamento naquele momento. Qualquer mensagem SOAP que for enviada com um identificador de sessão inválido falhará, indicando que a sessão especificada não pode ser encontrada.  
  
 Se um **sessão** elemento não será enviado como parte de uma solicitação SOAP, o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância implicitamente inicia uma sessão durante a **Discover** ou **Execute** chamada de método e finalizará essa sessão assim que a chamada do método for concluída.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento EndSession &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md)   
 [Gerenciando conexões e sessões &#40; XMLA &#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Cabeçalhos &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)  
  
  
