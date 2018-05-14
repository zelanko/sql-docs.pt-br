---
title: Elemento Return (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eb01fa78d1542cb2a791fe0ab00b839ab1a8e8bf
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="return-element-xmla"></a>Elemento return (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contém informações retornadas por uma [DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md) elemento em resposta a um [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) chamada de método ou um [ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md) elemento em resposta a um [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) chamada de método.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DiscoverResponse> <!-- or ExecuteResponse -->  
   <return>  
      <root>...</root>  
      <!-- or -->  
      <results>...</results> <!-- ExecuteResponse only -->  
   </return>  
</DiscoverResponse>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md), [ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md)|  
|Elementos filho|Veja a tabela abaixo.|  
  
|Ancestor|Elementos filho|  
|--------------|--------------------|  
|[DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)|[raiz](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
|[ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md)|[raiz](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) ou [resultados](../../../analysis-services/xmla/xml-elements-properties/results-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 O **retornar** elemento contém os dados retornados pelo **Discover** e **Execute** métodos. Normalmente, o **retornar** elemento contém um único **raiz** elemento que contém os dados retornados por uma bem-sucedida **Discover** ou **Execute** um XML para exceção Analysis (XMLA) retornado por uma chamada de método malsucedida ou chamada de método. Se o **Execute** método contém um **lote** comando que executa várias operações, o **retornar** elemento contém um **resultados** elemento que, por sua vez, contém um **raiz** elemento para cada comando executado com êxito ou não pelo **lote** comando.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
