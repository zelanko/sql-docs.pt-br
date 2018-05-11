---
title: Tipo de dados MDDataSet (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bd82c473b768d8359c82bd2cf55c1cf27e76ae3f
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="mddataset-data-type-xmla"></a>Tipo de dados MDDataSet (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
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
  
## <a name="remarks"></a>Remarks  
 O **MDDataSet** tipo de dados fornece o orientado para OLAP conjunto de linhas (ou conjunto de dados) necessários para representar dados OLAP em XML. O conteúdo desse conjunto de linhas pode variar dependendo dos valores da **conteúdo** e **formato** propriedades fornecidas a [propriedades](../../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md) coleção do  **Executar** método. Para obter mais informações sobre o **conteúdo** e **formato** propriedades, consulte [propriedades com suporte do XMLA &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).  
  
 Para obter informações básicas sobre o comando OLE DB para estruturas de conjuntos de dados OLAP, consulte “Mapeamento do tipo de dados MDDataSet para OLE DB” na especificação do XML for Analysis 1.1. Para obter um exemplo completo de linguagem XSD de definição de esquema XML do **MDDataSet** tipo de dados, consulte "Exemplo de MDDataSet do apêndice d:" da especificação XML for Analysis 1.1.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML &#40;XMLA&#41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)  
  
  
