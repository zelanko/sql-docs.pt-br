---
title: Elemento DeleteWithDescendants (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- DeleteWithDescendants Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#DeleteWithDescendants
- microsoft.xml.analysis.deletewithdescendants
- urn:schemas-microsoft-com:xml-analysis#DeleteWithDescendants
helpviewer_keywords:
- DeleteWithDescendants element
ms.assetid: adfc9437-aaa7-4364-bcdb-128fcc9a410d
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3abfe75505b2eba397a75b0d996a868df01caefe
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="deletewithdescendants-element-xmla"></a>Elemento DeleteWithDescendants (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Indica se os descendentes de membros de atributo também são excluídos pelo comando pai [Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Drop>  
   ...  
   <DeleteWithDescendants>...</DeleteWithDescendants>  
   ...  
</Drop>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Boolean|  
|Valor padrão|False|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 O elemento **DeleteWithDescendants** determina se o comando **Drop** não deve apenas excluir os membros de atributo identificados pelo elemento [Where](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md) , mas também que os descendentes daqueles membros de atributo devem ser descartados.  
  
> [!NOTE]  
>  Esse elemento só se aplica a membros de atributos nas hierarquias pai-filho.  
  
 Para obter mais informações sobre a exclusão e atualização de membros de atributo, consulte [Inserindo, atualizando e descartando membros &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
