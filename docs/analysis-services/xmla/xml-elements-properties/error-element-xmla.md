---
title: Elemento Error (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f223bff2dced01c2b3f954ca14242b1a35c93813
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38036644"
---
# <a name="error-element-xmla"></a>Elemento Error (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contém informações sobre o erro retornado por uma instância do Analysis Services.  
  
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Mensagem](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|  
|Elementos filho|Veja a tabela abaixo.|  
  
|Ancestor|Elementos filho|  
|--------------|--------------------|  
|[Mensagem](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|Nenhum|  
|[Célula](../../../analysis-services/xmla/xml-elements-properties/cell-element-mddataset-xmla.md), [linha](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|[Descrição](../../../analysis-services/xmla/xml-elements-properties/description-element-xmla.md), [ErrorCode](../../../analysis-services/xmla/xml-elements-properties/errorcode-element-xmla.md), [HelpFile](../../../analysis-services/xmla/xml-elements-properties/helpfile-element-xmla.md), [fonte](../../../analysis-services/xmla/xml-elements-properties/source-element-error-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|attribute|Description|  
|---------------|-----------------|  
|ErrorCode|Exigido **UnsignedInt** atributo (somente quando **mensagem** é o elemento pai.) Contém o código de retorno numérico do erro.|  
|Severity|Opcional **cadeia de caracteres** atributo (somente quando **mensagem** é o elemento pai.) Contém a gravidade do erro.|  
|Description|Opcional **cadeia de caracteres** atributo (somente quando **mensagem** é o elemento pai.) Contém o texto descritivo do erro.|  
|Origem|Opcional **cadeia de caracteres** atributo (somente quando **mensagem** é o elemento pai.) Contém o nome do componente que gerou o erro.|  
|HelpFile|Opcional **cadeia de caracteres** atributo (somente quando **mensagem** é o elemento pai.) Contém o caminho ou a URL para o arquivo de Ajuda ou tópico que descreve o erro.|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>Confira também
 [Elemento Warning &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/warning-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
