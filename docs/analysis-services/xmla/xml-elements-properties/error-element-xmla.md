---
title: Elemento Error (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
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
ms.openlocfilehash: 95adf11f3582f58a9d8ba76072d3d99bdaaf1bb9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="error-element-xmla"></a>Elemento Error (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contém informações sobre um erro retornado por uma instância de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
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
|Elementos filho|Veja a tabela abaixo.|  
  
|Ancestor|Elementos filho|  
|--------------|--------------------|  
|[Mensagem](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|Nenhuma|  
|[Cell](../../../analysis-services/xmla/xml-elements-properties/cell-element-mddataset-xmla.md), [row](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|[Description](../../../analysis-services/xmla/xml-elements-properties/description-element-xmla.md), [ErrorCode](../../../analysis-services/xmla/xml-elements-properties/errorcode-element-xmla.md), [HelpFile](../../../analysis-services/xmla/xml-elements-properties/helpfile-element-xmla.md), [Source](../../../analysis-services/xmla/xml-elements-properties/source-element-error-xmla.md)|  
  
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
 [Elemento Warning & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/warning-element-xmla.md)   
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
