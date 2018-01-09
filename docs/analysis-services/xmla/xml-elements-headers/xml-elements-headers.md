---
title: "Cabeçalhos (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
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
ms.openlocfilehash: 2006ca27d9a11924e053087b6a35d3d4df26d7d8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="xml-elements---headers"></a>Elementos XML - cabeçalhos
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]O protocolo XML for Analysis (XMLA) usa elementos XML no cabeçalho SOAP para gerenciar recursos de nível de protocolo, como suporte de sessão e a negociação de recursos com suporte.  
  
## <a name="in-this-section"></a>Nesta seção  
 Os tópicos a seguir descrevem os elementos de cabeçalho XMLA implementados por [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
|Método|Description|  
|------------|-----------------|  
|[Elemento BeginSession &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md)|Usa um cabeçalho SOAP em um mensagem de solicitação SOAP para iniciar uma sessão nova em uma instância de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento EndSession &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md)|Usa o cabeçalho SOAP em uma mensagem de solicitação SOAP para terminar uma sessão existente em uma instância de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento Session &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md)|Usa o cabeçalho SOAP em uma mensagem de solicitação SOAP para identificar uma sessão existente explícita em uma instância de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento ProtocolCapabilities &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/protocolcapabilities-element-xmla.md)|Usa o cabeçalho SOAP em uma mensagem de solicitação SOAP para identificar os recursos do protocolo entre uma instância de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e um aplicativo cliente.|  
  
## <a name="see-also"></a>Consulte Também  
 [Elementos XML &#40; XMLA &#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [Tipos de dados XML &#40; XMLA &#41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [Elementos XML &#40; XMLA &#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)  
  
  
