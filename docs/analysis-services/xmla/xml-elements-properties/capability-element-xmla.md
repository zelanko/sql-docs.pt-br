---
title: Elemento capability (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile"
ms.openlocfilehash: a53bcd66141dfb367cc54239d9d8faab0e0e6576
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="capability-element-xmla"></a>Elemento Capability (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Indica suporte para uma capacidade de protocolo no elemento de cabeçalho pai [ProtocolCapabilities](../../../analysis-services/xmla/xml-elements-headers/protocolcapabilities-element-xmla.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ProtocolCapabilities>  
   ...  
   <Capability>...</Capability>  
   ...  
</ProtocolCapabilities>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[ProtocolCapabilities](../../../analysis-services/xmla/xml-elements-headers/protocolcapabilities-element-xmla.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 O **recurso** elemento indica que um recurso específico, como binário ou compactação, tem suporte no aplicativo que incluído o **ProtocolCapabilities** elemento de cabeçalho no Cabeçalho SOAP da solicitação SOAP ou pela instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que incluído o **ProtocolCapabilities** elemento de cabeçalho no cabeçalho SOAP da resposta SOAP. O valor do elemento **Capability** é o nome do recurso com suporte.  
  
 O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] oferece suporte aos recursos listados na tabela a seguir.  
  
|Nome do recurso|Descrição|  
|---------------------|-----------------|  
|sx|Suporte a XML binário|  
|xpress|Suporte à compactação|  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando conexões e sessões & #40; XMLA & #41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
