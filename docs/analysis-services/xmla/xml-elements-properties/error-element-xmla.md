---
title: Elemento Error (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
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
apiname:
- Error Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.error
- http://schemas.microsoft.com/analysisservices/2003/engine#Error
- urn:schemas-microsoft-com:xml-analysis#Error
helpviewer_keywords:
- Error element
ms.assetid: add670cb-cab2-42be-91a3-d0c385f29d16
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 214dc93af2f02f4bd47ac9d0199b0254fe2ab024
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="error-element-xmla"></a>Elemento Error (XMLA)
  Contém informações sobre o erro retornado por uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Message>  
   <Error   
      ErrorCode="unsignedint"   
      Severity="string"   
      Description="string"  
      Source="string"  
      HelpFile="string"  
   />  
</Message>  
<!-- or -->  
<Cell><!-- or row -->  
   <!-- A child element -->  
      <Error xmlns="urn:schemas-microsoft-com:xml-analysis:exception"  
         < ErrorCode>...</ErrorCode>  
         < Description>...</Description>  
         < Source>...</Source>  
         < HelpFile>...</HelpFile>  
      </Error>  
   <!-- /A child element -- >  
</Cell>  
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
|Elementos pai|[Mensagem](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|  
|Elementos filho|Consulte a tabela a seguir.|  
  
|Ancestor|Elementos filho|  
|--------------|--------------------|  
|[Mensagem](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|Nenhuma|  
|[Célula](../../../analysis-services/xmla/xml-elements-properties/cell-element-mddataset-xmla.md), [linha](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|[Descrição](../../../analysis-services/xmla/xml-elements-properties/description-element-xmla.md), [ErrorCode](../../../analysis-services/xmla/xml-elements-properties/errorcode-element-xmla.md), [HelpFile](../../../analysis-services/xmla/xml-elements-properties/helpfile-element-xmla.md), [fonte](../../../analysis-services/xmla/xml-elements-properties/source-element-error-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|ErrorCode|Necessário **UnsignedInt** atributo (somente quando **mensagem** é o elemento pai.) Contém o código de retorno numérico do erro.|  
|Severity|Opcional **cadeia de caracteres** atributo (somente quando **mensagem** é o elemento pai.) Contém a gravidade do erro.|  
|Description|Opcional **cadeia de caracteres** atributo (somente quando **mensagem** é o elemento pai.) Contém o texto descritivo do erro.|  
|Origem|Opcional **cadeia de caracteres** atributo (somente quando **mensagem** é o elemento pai.) Contém o nome do componente que gerou o erro.|  
|HelpFile|Opcional **cadeia de caracteres** atributo (somente quando **mensagem** é o elemento pai.) Contém o caminho ou a URL para o arquivo de Ajuda ou tópico que descreve o erro.|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Warning &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/warning-element-xmla.md)   
 [Propriedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

