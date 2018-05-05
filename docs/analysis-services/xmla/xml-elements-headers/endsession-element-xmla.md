---
title: Elemento EndSession (XMLA) | Microsoft Docs
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
- EndSession Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#EndSession
- urn:schemas-microsoft-com:xml-analysis#EndSession
- microsoft.xml.analysis.endsession
helpviewer_keywords:
- EndSession element
ms.assetid: e64f1da4-5c83-40a2-b15e-837f5451bafa
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e773120f6d2a6323eb3c49877af00c3d8d57114e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="endsession-element-xmla"></a>Elemento EndSession (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Usa o cabeçalho SOAP em uma mensagem de solicitação SOAP para terminar uma sessão existente em uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 **Namespace** urn:schemas-microsoft-com:xml-analysis  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
   <soap:Header>  
      ...  
      <EndSession  
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
|SessionId|Atributo obrigatório **String** que identifica a sessão a ser encerrada. O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] usa um GUID (identificador global exclusivo) para identificar uma sessão.|  
  
## <a name="remarks"></a>Remarks  
 O **EndSession** elemento de cabeçalho é parte da solicitação SOAP enviada para uma sessão existente explicitamente iniciada um [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância. Se o elemento do cabeçalho **EndSession** for enviado, mas contiver um identificador de sessão que não seja mais válido, uma falha SOAP será retornada, indicando que a sessão não pode ser encontrada.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento BeginSession & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md)   
 [Elemento Session & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md)   
 [Gerenciando conexões e sessões & #40; XMLA & #41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Cabeçalhos & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)  
  
  
