---
title: Elemento ErrorConfiguration (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 68d5b3a5e1e381b1fb65a12c0aa77adf318a36b8
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34575158"
---
# <a name="errorconfiguration-element-xmla"></a>Elemento ErrorConfiguration (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Especifica as configurações de manipulação de erros que podem ocorrer durante uma [lote](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) ou [processo](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) operação.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Batch> <!-- or Process -->  
   ...  
   <ErrorConfiguration>  
      <KeyErrorLimit>...</KeyErrorLimit>  
      <KeyErrorLogFile>...</KeyErrorLogFile>  
      <KeyErrorAction>...</KeyErrorAction>  
      <KeyErrorLimitAction>...</KeyErrorLimitAction>  
      <KeyNotFound>...</KeyNotFound>  
      <KeyDuplicate>...</KeyDuplicate>  
      <NullKeyConvertedToUnknown>...</NullKeyConvertedToUnknown>  
      <NullKeyNotAllowed>...<NullKeyNotAllowed>  
   </ErrorConfiguration>  
   ...  
</Batch>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Batch](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md), [Process](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|  
|Elementos filho|[KeyDuplicate](../../../analysis-services/scripting/properties/keyduplicate-element-assl.md), [KeyErrorAction](../../../analysis-services/scripting/properties/keyerroraction-element-assl.md), [KeyErrorLimit](../../../analysis-services/scripting/properties/keyerrorlimit-element-assl.md), [KeyErrorLimitAction](../../../analysis-services/scripting/properties/keyerrorlimitaction-element-assl.md), [KeyErrorLogFile](../../../analysis-services/scripting/properties/keyerrorlogfile-element-assl.md), [ KeyNotFound](../../../analysis-services/scripting/properties/keynotfound-element-assl.md), [NullKeyConvertedToUnknown](../../../analysis-services/scripting/properties/nullkeyconvertedtounknown-element-assl.md), [NullKeyNotAllowed](../../../analysis-services/scripting/properties/nullkeynotallowed-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 A estrutura desse elemento é idêntica à estrutura do elemento **ErrorConfiguration** em ASSL (Analysis Services Scripting Language). Para obter mais informações sobre o **ErrorConfiguration** elemento, consulte [elemento ErrorConfiguration &#40;ASSL&#41;](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md).  
  
## <a name="see-also"></a>Confira também
 [Propriedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
