---
title: Cabeçalhos (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
- apinav
helpviewer_keywords:
- XMLA, headers
- SOAP headers [XML for Analysis]
- XML for Analysis, headers
- headers [XML for Analysis]
ms.assetid: 36407b5c-d98d-47e4-8d36-d8896e15a748
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fdc6c9ebfef18b108c31870c5703cac3841cfc29
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48155683"
---
# <a name="headers-xmla"></a>Cabeçalhos (XMLA)
  O protocolo XML for Analysis (XMLA) usa elementos XML no cabeçalho SOAP para gerenciar recursos em nível de protocolo, como um suporte à sessão e a negociação de recursos com suporte.  
  
## <a name="in-this-section"></a>Nesta seção  
 Os tópicos a seguir descrevem os elementos de cabeçalho XMLA implementados por [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
|Método|Description|  
|------------|-----------------|  
|[Elemento BeginSession &#40;XMLA&#41;](session-element-xmla.md)|Usa um cabeçalho SOAP em um mensagem de solicitação SOAP para iniciar uma sessão nova em uma instância de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento EndSession &#40;XMLA&#41;](endsession-element-xmla.md)|Usa o cabeçalho SOAP em uma mensagem de solicitação SOAP para terminar uma sessão existente em uma instância de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento Session &#40;XMLA&#41;](session-element-xmla.md)|Usa o cabeçalho SOAP em uma mensagem de solicitação SOAP para identificar uma sessão existente explícita em uma instância de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento ProtocolCapabilities &#40;XMLA&#41;](protocolcapabilities-element-xmla.md)|Usa o cabeçalho SOAP em uma mensagem de solicitação SOAP para identificar os recursos do protocolo entre uma instância de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e um aplicativo cliente.|  
  
## <a name="see-also"></a>Consulte também  
 [Elementos XML &#40;XMLA&#41;](../../dev-guide/xml-elements-xmla.md)   
 [Tipos de dados XML &#40;XMLA&#41;](../xml-data-types/xml-data-types-xmla.md)   
 [Elementos XML &#40;XMLA&#41;](../../dev-guide/xml-elements-xmla.md)  
  
  
