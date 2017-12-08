---
title: O elemento CellOrdinal (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
apiname: CellOrdinal Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.cellordinal
- urn:schemas-microsoft-com:xml-analysis#CellOrdinal
- http://schemas.microsoft.com/analysisservices/2003/engine#CellOrdinal
helpviewer_keywords: CellOrdinal element
ms.assetid: 1808c498-e3b4-4e5c-9e22-7f8662d32874
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d4fee3f8cfb4bc664734944316c4fcb9996d2a2c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="cellordinal-element-xmla"></a>Elemento CellOrdinal (XMLA)
  Contém a posição ordinal dentro de um cubo de uma célula a ser atualizada por um [UpdateCells](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md) comando.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Cell>  
   ...  
   <CellOrdinal>...</CellOrdinal>  
   ...  
</Cell>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Longo|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Célula](../../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O **CellOrdinal** elemento identifica a célula a ser atualizada pelo **UpdateCells** comando.  
  
 Para obter mais informações sobre atualização de células, consulte [Atualizando células &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/updating-cells-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de valor &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/value-element-xmla.md)   
 [Elemento UpdateCells &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)   
 [Propriedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
