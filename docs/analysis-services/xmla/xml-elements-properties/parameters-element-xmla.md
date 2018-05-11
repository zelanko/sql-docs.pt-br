---
title: Elemento Parameters (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 133920742ad3815907af1cdc2d221f169ce238f1
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="parameters-element-xmla"></a>Elemento Parameters (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contém uma coleção de [parâmetro](../../../analysis-services/xmla/xml-elements-properties/parameter-element-xmla.md) elementos usados pelo [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) método.  
  
 **Namespace:**`urn:schemas-microsoft-com:xml-analysis`  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Execute>  
...  
   <Parameters>  
      <Parameter>...</Parameter>  
   </Parameters>  
...  
</Execute>  
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
|Elementos pai|[Execute (executar)](../../../analysis-services/xmla/xml-elements-methods-execute.md)|  
|Elementos filho|[Parâmetro](../../../analysis-services/xmla/xml-elements-properties/parameter-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 Alguns comandos do XMLA (XML for Analysis), como o comando [Process](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) , podem requerer informações adicionais. O **parâmetros** elemento fornece um mecanismo para fornecer informações adicionais, incluindo partes de informações de um comando XMLA.  
  
 Se o comando XMLA não usar o **parâmetros** elemento, o elemento pode ser omitido ao chamar o **Execute** método.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
