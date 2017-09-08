---
title: "Cabeçalhos (XMLA) | Microsoft Docs"
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
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- XMLA, headers
- SOAP headers [XML for Analysis]
- XML for Analysis, headers
- headers [XML for Analysis]
ms.assetid: 36407b5c-d98d-47e4-8d36-d8896e15a748
caps.latest.revision: 14
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b12c8b2b22d51069998b4b49d1c9aceb43f063a5
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="xml-elements---headers"></a>Elementos XML - cabeçalhos
  O protocolo XML for Analysis (XMLA) usa elementos XML no cabeçalho SOAP para gerenciar recursos em nível de protocolo, como um suporte à sessão e a negociação de recursos com suporte.  
  
## <a name="in-this-section"></a>Nesta seção  
 Os tópicos a seguir descrevem os elementos de cabeçalho XMLA implementados por [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
|Método|Description|  
|------------|-----------------|  
|[Elemento BeginSession &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md)|Usa um cabeçalho SOAP em um mensagem de solicitação SOAP para iniciar uma sessão nova em uma instância de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento EndSession &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md)|Usa o cabeçalho SOAP em uma mensagem de solicitação SOAP para terminar uma sessão existente em uma instância de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento Session &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md)|Usa o cabeçalho SOAP em uma mensagem de solicitação SOAP para identificar uma sessão existente explícita em uma instância de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento ProtocolCapabilities &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/protocolcapabilities-element-xmla.md)|Usa o cabeçalho SOAP em uma mensagem de solicitação SOAP para identificar os recursos do protocolo entre uma instância de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e um aplicativo cliente.|  
  
## <a name="see-also"></a>Consulte também  
 [Elementos XML &#40; XMLA &#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [Tipos de dados XML &#40; XMLA &#41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [Elementos XML &#40; XMLA &#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)  
  
  
