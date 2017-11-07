---
title: Tipo de dados MDDataSet (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MDDataSet Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#MDDataSet
- MDDataSet
- urn:schemas-microsoft-com:xml-analysis#MDDataSet
helpviewer_keywords:
- MDDataSet data type
ms.assetid: 1a7e0092-f9f0-4ae5-ba27-ad1d8ebe8cb9
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6ed0c285f34f55f89b571cf671cf6601e5a81490
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="mddataset-data-type-xmla"></a>Tipo de dados MDDataSet (XMLA)
  Define um tipo de dados derivado que representa dados multidimensionais retornados pelo [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) método.  
  
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|[Conjunto de resultados](../../../analysis-services/xmla/xml-data-types/resultset-data-type-xmla.md)|  
|Tipos de dados derivados|Nenhuma|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|[Eixos](../../../analysis-services/xmla/xml-elements-properties/axes-element-xmla.md), [CellData](../../../analysis-services/xmla/xml-elements-properties/celldata-element-xmla.md), [OlapInfo](../../../analysis-services/xmla/xml-elements-properties/olapinfo-element-xmla.md)|  
|Elementos derivados|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O **MDDataSet** tipo de dados fornece o orientado para OLAP conjunto de linhas (ou conjunto de dados) necessários para representar dados OLAP em XML. O conteúdo desse conjunto de linhas pode variar dependendo dos valores da **conteúdo** e **formato** propriedades fornecidas a [propriedades](../../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md) coleção do  **Executar** método. Para obter mais informações sobre o **conteúdo** e **formato** propriedades, consulte [suporte para propriedades de XMLA &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).  
  
 Para obter informações básicas sobre o comando OLE DB para estruturas de conjuntos de dados OLAP, consulte “Mapeamento do tipo de dados MDDataSet para OLE DB” na especificação do XML for Analysis 1.1. Para obter um exemplo completo de linguagem XSD de definição de esquema XML do **MDDataSet** tipo de dados, consulte "Exemplo de MDDataSet do apêndice d:" da especificação XML for Analysis 1.1.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML &#40; XMLA &#41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)  
  
  

