---
title: Tipo de dados MDDataSet (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MDDataSet Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#MDDataSet
- MDDataSet
- urn:schemas-microsoft-com:xml-analysis#MDDataSet
helpviewer_keywords:
- MDDataSet data type
ms.assetid: 1a7e0092-f9f0-4ae5-ba27-ad1d8ebe8cb9
caps.latest.revision: 27
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9c1580365cc6c7949c552333728b5083b96f7ef9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37165317"
---
# <a name="mddataset-data-type-xmla"></a>Tipo de dados MDDataSet (XMLA)
  Define um tipo de dados derivado que representa dados multidimensionais retornados pelo [Execute](../xml-elements-methods-execute.md) método.  
  
 **Namespace** urn: schemas-microsoft-com: XML-análise: mddataset  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">  
   <!-- The following elements extend Resultset -->  
   <!-- Optional schema elements -->  
   <OlapInfo>...</OlapInfo>  
   <Axes>...</Axes>  
   <CellData>...</CellData>  
</root>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|[Conjunto de resultados](resultset-data-type-xmla.md)|  
|Tipos de dados derivados|Nenhum|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhum|  
|Elementos filho|[Eixos](../xml-elements-properties/axes-element-xmla.md), [CellData](../xml-elements-properties/celldata-element-xmla.md), [OlapInfo](../xml-elements-properties/olapinfo-element-xmla.md)|  
|Elementos derivados|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O tipo de dados `MDDataSet` fornece o conjunto de linhas (ou conjunto de dados) orientado para OLAP exigido para representar dados OLAP em XML. O conteúdo desse conjunto de linhas pode variar dependendo dos valores da `Content` e `Format` propriedades fornecidas a [propriedades](../xml-elements-properties/properties-element-xmla.md) coleção do `Execute` método. Para obter mais informações sobre o `Content` e `Format` propriedades, consulte [propriedades XMLA com suporte &#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md).  
  
 Para obter informações básicas sobre o comando OLE DB para estruturas de conjuntos de dados OLAP, consulte “Mapeamento do tipo de dados MDDataSet para OLE DB” na especificação do XML for Analysis 1.1. Para obter um exemplo completo da linguagem XSD (XML Schema Definition) do tipo de dados `MDDataSet`, consulte o “Apêndice D: Exemplo de MDDataSet” da especificação do XML for Analysis 1.1.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML &#40;XMLA&#41;](xml-data-types-xmla.md)  
  
  
