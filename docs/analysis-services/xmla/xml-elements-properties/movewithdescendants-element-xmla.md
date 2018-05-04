---
title: Elemento MoveWithDescendants (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- MoveWithDescendants Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.movewithdescendants
- http://schemas.microsoft.com/analysisservices/2003/engine#MoveWithDescendants
- urn:schemas-microsoft-com:xml-analysis#MoveWithDescendants
helpviewer_keywords:
- MoveWithDescendants element
ms.assetid: d02285b6-1801-4da9-8e2b-9ab008e25558
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 7f6a40dd9485ff4a3c82ae82a7d75e54f03cb039
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="movewithdescendants-element-xmla"></a>Elemento MoveWithDescendants (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Indica se os descendentes de membros de atributo também são atualizados pelo pai [atualização](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md) comando.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Update>  
   ...  
   <MoveWithDescendants>...</MoveWithDescendants>  
   ...  
</Update>  
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
|Elementos pai|[Update (atualizar)](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 O **MoveWithDescendants** elemento determina se o **atualizar** comando não deve apenas atualizar os membros de atributo identificados pelo [atributos](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md) elemento, mas também que os descendentes daqueles membros de atributo devem ser atualizados.  
  
> [!NOTE]  
>  Esse elemento só se aplica a membros de atributos nas hierarquias pai-filho.  
  
 Para obter mais informações sobre como atualizar membros, consulte [inserindo, atualizando e descartando membros &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
