---
title: Elemento capability (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Capability Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Capability
- http://schemas.microsoft.com/analysisservices/2003/engine#Capability
- microsoft.xml.analysis.capability
helpviewer_keywords:
- Capability element
ms.assetid: 544a733e-77fc-48a0-8f92-9cd1fdbcf824
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7c6fd189a44ec34283e87cd220f2c582f982ffa9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48105336"
---
# <a name="capability-element-xmla"></a>Elemento Capability (XMLA)
  Indica que há suporte para um recurso de protocolo no pai [ProtocolCapabilities](../xml-elements-headers/protocolcapabilities-element-xmla.md) elemento de cabeçalho.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ProtocolCapabilities>  
   ...  
   <Capability>...</Capability>  
   ...  
</ProtocolCapabilities>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|None|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[ProtocolCapabilities](../xml-elements-headers/protocolcapabilities-element-xmla.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O `Capability` elemento indica que um recurso específico, como binário ou compactação, há suporte para qualquer aplicativo que incluiu o `ProtocolCapabilities` elemento de cabeçalho no cabeçalho SOAP da solicitação SOAP ou pela instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que incluído o `ProtocolCapabilities` elemento de cabeçalho no cabeçalho SOAP da resposta SOAP. O valor do elemento `Capability` é o nome do recurso com suporte.  
  
 O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] oferece suporte aos recursos listados na tabela a seguir.  
  
|Nome do recurso|Description|  
|---------------------|-----------------|  
|sx|Suporte a XML binário|  
|xpress|Suporte à compactação|  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando conexões e sessões &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
