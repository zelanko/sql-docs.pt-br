---
title: Valor de elemento (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fa5a552bc756abee0e8755ebd7b4c107da4ea7c0
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="value-element-xmla"></a>Elemento Value (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contém o valor desejado de um [atributo](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md) elemento a ser adicionado por um [inserir](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md) comando, ou um [célula](../../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md) elemento a ser atualizada por um [UpdateCells](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)comando.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Attribute> <!-- or Cell --!>  
   ...  
   <Value>...</Value>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Any (qualquer)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Atributo](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md), [célula](../../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 Para **atributo** elementos, o **valor** elemento contém o valor desejado que o membro deve conter depois o **inserir** comando é confirmado. Para obter mais informações sobre a inserção de membros, consulte [inserindo, atualizando e descartando membros &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md).  
  
 Para **célula** elementos, o **valor** elemento contém o valor desejado que a célula deve conter depois o **UpdateCells** comando é confirmado. O valor real armazenado na tabela de writeback para aquela célula é a diferença entre o valor original da célula e o valor desejado da célula.  
  
 O tipo de dados usado por este elemento deve corresponder ao tipo de dados da célula a ser atualizado.  
  
 Para obter mais informações sobre atualização de células, consulte [Atualizando células &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/updating-cells-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [O elemento CellOrdinal &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/cellordinal-element-xmla.md)   
 [Inserir o elemento & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Elemento UpdateCells & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)   
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
