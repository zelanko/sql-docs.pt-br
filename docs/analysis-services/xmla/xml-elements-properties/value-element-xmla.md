---
title: Valor de elemento (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Value Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.value
- urn:schemas-microsoft-com:xml-analysis#Value
- http://schemas.microsoft.com/analysisservices/2003/engine#Value
helpviewer_keywords: Value element
ms.assetid: f87ca7f8-d9fe-4730-a706-5d50fcfe21df
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d40497916d4ec482fae217dfbddac4a12bd011d0
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="value-element-xmla"></a>Elemento Value (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Contém o valor desejado de um [atributo](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md) elemento a ser adicionado por um [inserir](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md) comando, ou um [célula](../../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md) elemento a ser atualizada por um [UpdateCells](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md) comando.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Attribute> <!-- or Cell --!>  
   ...  
   <Value>...</Value>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Any (qualquer)|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Atributo](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md), [célula](../../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Para **atributo** elementos, o **valor** elemento contém o valor desejado que o membro deve conter depois o **inserir** comando é confirmado. Para obter mais informações sobre a inserção de membros, consulte [inserir, atualizar e remover membros &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md).  
  
 Para **célula** elementos, o **valor** elemento contém o valor desejado que a célula deve conter depois o **UpdateCells** comando é confirmado. O valor real armazenado na tabela de writeback para aquela célula é a diferença entre o valor original da célula e o valor desejado da célula.  
  
 O tipo de dados usado por este elemento deve corresponder ao tipo de dados da célula a ser atualizado.  
  
 Para obter mais informações sobre atualização de células, consulte [Atualizando células &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/updating-cells-xmla.md).  
  
## <a name="see-also"></a>Consulte Também  
 [O elemento CellOrdinal &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/cellordinal-element-xmla.md)   
 [Inserir o elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Elemento UpdateCells &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)   
 [Propriedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
