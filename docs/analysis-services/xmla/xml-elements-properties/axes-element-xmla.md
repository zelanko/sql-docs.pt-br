---
title: Eixos elemento (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 02b9c91f30c45e59d0f5eba00a5b76262070d711
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="axes-element-xmla"></a>Elemento Axes (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contém uma coleção de [eixo](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md) elementos que representam dados de eixo contidos por um [raiz](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) elemento que usa o [MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md) tipo de dados.  
  
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
|Elementos filho|[Eixo](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 Sob o **eixos** elemento, o **eixo** elementos são listados na ordem em que eles ocorrem no conjunto de dados, começando com zero. O **AxisFormat** XMLA propriedade determina como **eixo** elementos são formatados. Para obter mais informações sobre o **AxisFormat** propriedade, consulte [propriedades com suporte do XMLA &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).  
  
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
 [Tipo de dados MDDataSet & #40; XMLA & #41;](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)   
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
