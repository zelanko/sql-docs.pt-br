---
title: Elemento Warning (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 73662315d294cade8b344f8967923fe15e94f886
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34576728"
---
# <a name="warning-element-xmla"></a>Elemento Warning (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contém informações sobre um aviso retornado por uma instância do Analysis Services.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Message>  
   <Warning   
      ErrorCode="unsignedint"   
      Severity="string"   
      Description="string"  
      Source="string"  
      HelpFile="string"  
   />  
</Message>  
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
|Elementos filho|Nenhum|  
  
## <a name="attributes"></a>Atributos  
  
|attribute|Description|  
|---------------|-----------------|  
|ErrorCode|Atributo **UnsignedInt** obrigatório. Contém o código de retorno numérico do aviso.|  
|Severity|Atributo **String** opcional. Contém a severidade do aviso.|  
|Description|Atributo **String** opcional. Contém o texto descritivo do aviso.|  
|Origem|Atributo **String** opcional. Contém o nome do componente que gerou o aviso.|  
|HelpFile|Atributo **String** opcional. Contém o caminho ou a URL para o arquivo de Ajuda ou tópico que descreve o aviso.|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>Confira também
 [Elemento Error &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
