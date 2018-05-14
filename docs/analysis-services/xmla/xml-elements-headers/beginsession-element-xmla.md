---
title: Elemento BeginSession (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: aace4a6f0f8bfbf1cf41853224b98b0dd09fa26a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="beginsession-element-xmla"></a>Elemento BeginSession (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
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
  
## <a name="remarks"></a>Remarks  
 O **BeginSession** elemento de cabeçalho é parte de uma solicitação SOAP enviada a um [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância e inicia explicitamente uma nova sessão na instância. O cabeçalho SOAP retornado pela resposta de SOAP contém um [sessão](../../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md) elemento que identifica a nova sessão. Esse identificador de nova sessão é armazenado e enviado em solicitações SOAP subsequentes usando o **sessão** elemento de cabeçalho.  
  
 Se o **BeginSession** elemento de cabeçalho não é enviado, uma sessão não será iniciada explicitamente. Se uma sessão não for iniciada explicitamente, as transações não poderão ser gerenciadas naquela sessão. Em outras palavras, você não pode usar o seguinte XML para comandos Analysis (XMLA): [BeginTransaction](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md), [CommitTransaction](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md), e [RollbackTransaction](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md). Todos os métodos e comandos XMLA executados em uma sessão iniciada implicitamente são considerados transações atômicas.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento EndSession & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md)   
 [Elemento Session & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md)   
 [Gerenciando conexões e sessões & #40; XMLA & #41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Cabeçalhos & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)  
  
  
