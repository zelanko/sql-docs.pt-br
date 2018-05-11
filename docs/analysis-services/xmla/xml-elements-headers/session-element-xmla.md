---
title: Elemento Session (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eca14da555b90b90f692eec384939578d30bd89d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="session-element-xmla"></a>Elemento Session (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Usa o cabeçalho SOAP em uma mensagem de solicitação SOAP para identificar uma sessão existente explícita em uma instância de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
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
  
## <a name="remarks"></a>Remarks  
 O **sessão** elemento de cabeçalho identifica uma sessão existente explicitamente iniciada na [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância. O elemento **Session** faz parte do cabeçalho SOAP nos seguintes tipos de mensagens:  
  
-   Uma resposta SOAP que contém um elemento de cabeçalho SOAP [BeginSession](../../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md) .  
  
-   Uma solicitação SOAP para identificar a sessão na qual executar o método [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) ou [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) .  
  
 Um identificador de sessão não garante que uma sessão permaneça válida. A sessão especificada no elemento **Session** pode expirar. Por exemplo, uma sessão pode expirar se o tempo da sessão atingir seu limite ou se a conexão associada à sessão for interrompida. Se a sessão expirar e não for mais válida, o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] finalizará a sessão e reverterá as transações que estiverem em andamento naquele momento. Qualquer mensagem SOAP que for enviada com um identificador de sessão inválido falhará, indicando que a sessão especificada não pode ser encontrada.  
  
 Se um **sessão** elemento não será enviado como parte de uma solicitação SOAP, o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância implicitamente inicia uma sessão durante a **Discover** ou **Execute** chamada de método e finalizará essa sessão assim que a chamada do método for concluída.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento EndSession & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md)   
 [Gerenciando conexões e sessões & #40; XMLA & #41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Cabeçalhos & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)  
  
  
