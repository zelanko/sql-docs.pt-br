---
title: Tipo de dados EnumString (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- EnumString Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- EnumString
- urn:schemas-microsoft-com:xml-analysis#EnumString
- http://schemas.microsoft.com/analysisservices/2003/engine#EnumString
helpviewer_keywords:
- EnumString data type
ms.assetid: 9214195e-4539-419b-95ec-b7aa75e033ab
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 034ebe0218a8effece3aee526f9920850a7df536
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117501"
---
# <a name="enumstring-data-type-xmla"></a>Tipo de dados EnumString (XMLA)
  Define um tipo de dados derivado que representa um conjunto de constantes nomeadas para um determinado enumerador.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<EnumString>...</EnumString>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|`string`|  
|Tipos de dados derivados|Nenhum|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhum|  
|Elementos filho|Nenhum|  
|Elementos derivados|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 XMLA (XML for Analysis) usa enumeração para limitar os valores de cadeia para um conjunto de configurações verificáveis. `EnumString` usa o tipo de dados XML `string` padrão. São especificados os valores específicos para cada uma das constantes nomeadas com a definição de enumerador. Enumeradores são definidos pela inclusão deles para o [DISCOVER_ENUMERATORS](../../schema-rowsets/xml/discover-enumerators-rowset.md) linhas de esquema e pode ser recuperado usando o [Discover](../xml-elements-methods-discover.md) tipo de solicitação de método com o DISCOVER_ENUMERATORS.  
  
 A tabela a seguir descreve os enumeradores suportados por uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
|Enumerador|Description|  
|----------------|-----------------|  
|ProviderType|Oferece suporte à coluna ProviderType no [DISCOVER_DATASOURCES](../../schema-rowsets/xml/discover-datasources-rowset.md) de linhas de esquema, que determina o tipo de dados que podem ser retornados por uma [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância.<br /><br /> Esta enumeração também aceita a propriedade XMLA, `ProviderType` que determina os tipos de provedor com suporte em uma instância [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Essa enumeração também é usada no conjunto de linhas de esquema DISCOVER_DATASOURCES.<br /><br /> Para obter mais informações sobre `ProviderType`, consulte [propriedades com suporte do XMLA &#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
|AuthenticationMode|Fornece suporte à coluna AuthenticationMode no conjunto de linhas do esquema DISCOVER_DATASOURCES, que determina as credenciais de segurança que devem ser aprovadas para o acesso a uma instância [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|PropertyAccessType|Oferece suporte à coluna PropertyAccessType no [DISCOVER_PROPERTIES](../../schema-rowsets/xml/discover-properties-rowset.md) de linhas de esquema, que determina o tipo de acesso disponível para uma propriedade XMLA.|  
|StateSupport|Aceita a propriedade XMLA, `StateSupport`, que determina o nível de capacidade de manutenção de status do processo com suporte em uma instância [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].<br /><br /> Para obter mais informações sobre `StateSupport`, consulte [propriedades com suporte do XMLA &#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
|StateActionVerb|Contém uma lista de verbos aceitos por XMLA nos cabeçalhos SOAP e utilizados para iniciar, identificar e finalizar uma sessão.<br /><br /> Para obter mais informações sobre as sessões, consulte [Gerenciando conexões e sessões &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md).|  
|ResultsetFormat|Oferece suporte à propriedade XMLA, `Format`, que determina o tipo de dados retornados em uma [raiz](../xml-elements-properties/root-element-xmla.md) elemento.<br /><br /> Para obter mais informações sobre `Format`, consulte [propriedades com suporte do XMLA &#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
|ResultsetAxisFormat|Aceita a propriedade XMLA, `AxisFormat` que determina o formato das informações do eixo retornado em um elemento `root` que contém dados multidimensionais.<br /><br /> Para obter mais informações sobre `AxisFormat`, consulte [propriedades com suporte do XMLA &#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
|ResultsetContents|Aceita a propriedade XMLA, `Content` que determina se metadados ou dados são retornados em um elemento `root`.<br /><br /> Para obter mais informações sobre `Content`, consulte [propriedades com suporte do XMLA &#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
|MDXSupportLevel|Aceita a propriedade XMLA, `MDXSupport`, que indica o nível de suporte de MDX (Expressões multidimensional) disponível em uma instância [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].<br /><br /> Para obter mais informações sobre `MDXSupport`, consulte [propriedades com suporte do XMLA &#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML &#40;XMLA&#41;](xml-data-types-xmla.md)  
  
  