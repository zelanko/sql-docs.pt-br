---
title: Elemento capability (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile"
ms.openlocfilehash: dca8f668f64ab8ced157cf817be1f9f8f6390133
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38062974"
---
# <a name="capability-element-xmla"></a>Elemento Capability (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Indica que há suporte para um recurso de protocolo no pai [ProtocolCapabilities](../../../analysis-services/xmla/xml-elements-headers/protocolcapabilities-element-xmla.md) elemento de cabeçalho.  
  
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
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[ProtocolCapabilities](../../../analysis-services/xmla/xml-elements-headers/protocolcapabilities-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O **funcionalidade** elemento indica que um recurso específico, como binário ou compactação, há suporte para qualquer aplicativo que incluiu o **ProtocolCapabilities** elemento de cabeçalho no Cabeçalho SOAP da solicitação SOAP ou a instância do Analysis Services incluída a **ProtocolCapabilities** elemento de cabeçalho no cabeçalho SOAP da resposta SOAP. O valor do elemento **Capability** é o nome do recurso com suporte.  
  
 O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] oferece suporte aos recursos listados na tabela a seguir.  
  
|Nome do recurso|Description|  
|---------------------|-----------------|  
|sx|Suporte a XML binário|  
|xpress|Suporte à compactação|  
  
## <a name="see-also"></a>Confira também
 [Gerenciando conexões e sessões &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Propriedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
