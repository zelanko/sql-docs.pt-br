---
title: "Cabeçalhos (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- XMLA, headers
- SOAP headers [XML for Analysis]
- XML for Analysis, headers
- headers [XML for Analysis]
ms.assetid: 36407b5c-d98d-47e4-8d36-d8896e15a748
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 854d879b85ad5e70c21bd87240215b343aab96e7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
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
  
  
