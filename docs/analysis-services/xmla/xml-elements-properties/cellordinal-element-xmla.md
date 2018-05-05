---
title: O elemento CellOrdinal (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- CellOrdinal Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.cellordinal
- urn:schemas-microsoft-com:xml-analysis#CellOrdinal
- http://schemas.microsoft.com/analysisservices/2003/engine#CellOrdinal
helpviewer_keywords:
- CellOrdinal element
ms.assetid: 1808c498-e3b4-4e5c-9e22-7f8662d32874
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 75cda851fcf1d6af599d8297269f296590304fff
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="cellordinal-element-xmla"></a>Elemento CellOrdinal (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
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
  
## <a name="remarks"></a>Remarks  
 O **CellOrdinal** elemento identifica a célula a ser atualizada pelo **UpdateCells** comando.  
  
 Para obter mais informações sobre atualização de células, consulte [Atualizando células &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/updating-cells-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de valor & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/value-element-xmla.md)   
 [Elemento UpdateCells & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)   
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
