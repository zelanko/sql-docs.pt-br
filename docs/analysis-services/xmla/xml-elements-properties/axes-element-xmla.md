---
title: Eixos elemento (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Axes Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- Axes
- http://schemas.microsoft.com/analysisservices/2003/engine#Axes
- microsoft.xml.analysis.axes
- urn:schemas-microsoft-com:xml-analysis#Axes
helpviewer_keywords: Axes element
ms.assetid: 2005d06a-f8a2-4b4f-8c0d-2f7f73eb6f5c
caps.latest.revision: "21"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: facdfe5f8f4a03c5fcacff459dac78cb330f8f3b
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="axes-element-xmla"></a>Elemento Axes (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Contém uma coleção de [eixo](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md) elementos que representam dados de eixo contidos por um [raiz](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) elemento que usa o [MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md) tipo de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:mddataset">  
   ...  
   <Axes>  
      <Axis>...</Axis>  
   </Axes>  
   ...  
</root>  
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
|Elementos pai|[raiz](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
|Elementos filho|[Axis](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md)|  
  
## <a name="remarks"></a>Comentários  
 Sob o **eixos** elemento, o **eixo** elementos são listados na ordem em que eles ocorrem no conjunto de dados, começando com zero. O **AxisFormat** XMLA propriedade determina como **eixo** elementos são formatados. Para obter mais informações sobre o **AxisFormat** propriedade, consulte [suporte para propriedades de XMLA &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).  
  
 Um eixo representa um conjunto de tuplas no qual todas as tuplas têm a mesma dimensionalidade. Um conjunto pode ser representado de modos diferentes com vantagens diferentes. Por exemplo, o seguinte conjunto de quatro tuplas pode ser representado como uma coleção de tuplas bidimensionais ou o produto Cartesiano de dois conjuntos unidimensionais.  
  
|1999|1999|2000|2000|  
|----------|----------|----------|----------|  
|Real|Orçamento|Real|Orçamento|  
  
 Esse conjunto de tuplas pode ser representado como uma coleção de tuplas bidimensionais:  
  
```  
{ ( 1999, Actual ), ( 1999, Budget ), ( 2000, Actual ), ( 2000, Budget ) }  
```  
  
 Esse conjunto também pode ser representado como um produto Cartesiano de dois conjuntos unidimensionais:  
  
```  
{ 1999, 2000 } x { Actual, Budget }  
```  
  
 A primeira representação, tuplas bidimensionais, é mais simples para ser usada pelas ferramentas de cliente. A segunda representação, um produto Cartesiano de conjuntos unidimensionais, utiliza menos espaço e preserva a natureza multidimensional do conjunto.  
  
 A tabela a seguir lista operações que podem ser utilizadas para definir e caracterizar a estrutura e os membros de um eixo.  
  
|Operação|Description|  
|---------------|-----------------|  
|Membro|A unidade menor de um eixo que representa o membro de uma hierarquia da dimensão.|  
|Membros|Uma coleção de **membro** objetos da mesma hierarquia da dimensão.|  
|Tupla|Uma coleção de membros de diferentes hierarquias da dimensão.|  
|Tuplas|Uma coleção de **tupla** objetos com a mesma dimensionalidade.|  
|Union|Uma união de conjuntos.|  
|CrossJoin|Um produto Cartesiano de conjuntos.|  
  
 Essas operações traduzem as tuplas bidimensionais e o produto Cartesiano de conjuntos unidimensionais como se segue.  
  
## <a name="two-dimensional-tuples"></a>Tuplas bidimensionais  
  
```  
Tuples (  
   Tuple( Member(1999), Member(Actual) ),  
   Tuple( Member(1999), Member(Budget) ),  
   Tuple( Member(2000), Member(Actual) ),  
   Tuple( Member(2000), Member(Budget) )  
```  
  
## <a name="cartesian-product-of-one-dimensional-sets"></a>Produto Cartesiano de conjuntos unidimensionais  
  
```  
CrossProduct (  
   Members( Member(1999), Member(2000) ),  
   Members( Member(Actual), Member(Budget) )  
```  
  
 Um cliente pode usar o **AxisFormat** propriedade para solicitar uma representação específica.  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de dados MDDataSet &#40; XMLA &#41;](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)   
 [Propriedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
