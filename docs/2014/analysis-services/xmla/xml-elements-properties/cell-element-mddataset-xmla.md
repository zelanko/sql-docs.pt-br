---
title: Célula de elemento (MDDataSet) (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Cell Element (MDDataSet)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.cell
- http://schemas.microsoft.com/analysisservices/2003/engine#Cell
- urn:schemas-microsoft-com:xml-analysis#Cell
helpviewer_keywords:
- Cell element
ms.assetid: c4ea08a4-f653-4ade-be07-b91eb5b1ef32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7c422fdd13c03a2ab3c5a9cd58ce4cca1d22c5d6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48091666"
---
# <a name="cell-element-mddataset-xmla"></a>Elemento Cell (MDDataSet) (XMLA)
  Contém informações sobre uma única célula contida por um pai [CellData](celldata-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CellData>  
   <Cell CellOrdinal="unsignedInt">  
      <!-- Zero or more cell property values -->  
      <!-- or -->  
      <Error>...</Error>  
   </Cell>  
</CellData>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|None|  
|Valor padrão|None|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[CellData](celldata-element-xmla.md)|  
|Elementos filho|Zero ou mais valores de propriedade de célula ou [erro](error-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|attribute|Description|  
|---------------|-----------------|  
|CellOrdinal|Necessário `unsignedInt` atributo. A posição ordinal da célula dentro do conjunto de dados multidimensional.|  
  
## <a name="remarks"></a>Comentários  
 No elemento pai `root`, o elemento `Axes` é  seguido pelo elemento `CellData`, uma coleção de elementos `Cell` que contêm os valores de propriedade de  cada célula retornada no conjunto de dados multidimensionais. O elemento `Cell` contém o atributo `CellOrdinal`, que indica a posição ordinal baseada em zero da célula dentro do conjunto de dados multimensional e um elemento para cada valor de propriedade de célula associado à célula. Cada valor de propriedade de célula no `Cell` elemento é definido por um elemento XML separado. O valor da propriedade de célula é o dado contido pelo elemento XML, e o nome da propriedade de célula, conforme definido no elemento `CellInfo` do elemento raiz pai, corresponde ao nome do elemento XML.  
  
 A sintaxe a seguir descreve um valor de propriedade de célula.  
  
```  
<CellProperty xsi:type="string">value</CellProperty>  
```  
  
 O tipo de dados de um valor de propriedade de célula só é especificado para a propriedade de célula de VALUE. Os tipos de dados de outras propriedades de célula são determinados pela definição de propriedade de célula incluída no elemento `CellInfo`. Um elemento de valor de propriedade de célula poderá ser excluído se o valor padrão tiver sido especificado (incluindo um elemento `Default` para uma propriedade de célula contido no elemento `CellInfo`) para uma propriedade de célula ou se nenhum valor padrão tiver sido especificado e se o valor da propriedade da célula for nulo.  
  
## <a name="cell-property-errors"></a>Erros de propriedade de célula  
 Se uma propriedade de célula não pode ser retornada devido a um erro que ocorre na instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], como um erro de cálculo que impede que o valor que está sendo retornado para uma determinada célula, um `Error` elemento substitui o conteúdo da propriedade de célula em questão. O exemplo de XML a seguir descreve um erro de propriedade de célula:  
  
```  
<Cell CellOrdinal="0">  
   <Value xsi:type="xsd:double">  
      <Error>  
         <ErrorCode>2148497527</ErrorCode>  
         <Description>Unknown error</Description>  
      </Error>  
   </Value>  
</Cell>  
```  
  
## <a name="calculating-cell-ordinal-values"></a>Calculando valores ordinais de células  
 A referência de eixo para uma célula pode ser calculada com base em um valor de atributo `CellOrdinal`. Conceitualmente, as células são numeradas em um conjunto de dados como se o conjunto de dados fosse uma *p*-matriz dimensional, onde *p* é o número de eixos. As células são tratadas em ordem linha-principal.  
  
 Suponha que uma consulta solicite quatro medidas em colunas e uma interjunção de quatro estados com quatro quartos de linhas. Seguindo o resultado do conjunto de dados, a propriedade `CellOrdinal` da parte do resultado do conjunto de dados em negrito é o conjunto {9, 10, 11, 13, 14, 15, 17, 18, 19}. Esse é o conjunto, porque as células são numeradas em ordem de linha principal, começando com um `CellOrdinal` de 0 para a célula superior esquerda.  
  
|Estado|Quarter|Vendas de unidade|Custo na loja|Vendas da loja|Contas de vendas|  
|-----------|-------------|----------------|----------------|-----------------|-----------------|  
|Califórnia|T1|16890|14431.09|36175.2|5498|  
||2º TRIMESTRE|18052|15332.02|38396.75|5915|  
||T3|18370|**15672.83**|**39394.05**|**6014**|  
||T4|21436|**18094.5**|**45201.84**|**7015**|  
|Oregon|T1|19287|**16081.07**|**40170.29**|**6184**|  
||2º TRIMESTRE|15079|12678.96|31772.88|4799|  
||T3|16940|14273.78|35880.46|5432|  
||T4|16353|13738.68|34453.44|5196|  
|Washington|T1|30114|25240.08|63282.86|9906|  
||2º TRIMESTRE|29479|24953.25|62496.64|9654|  
||T3|30538|25958.26|64997.38|10007|  
||T4|34235|29172.72|73016.34|11217|  
  
 Aplicando a fórmula mostrada na figura, o eixo k = 0 tem Uk = 4 membros e o exio k = 1 tem Uk = 8 tuplas. P = 2 é o número total de eixos na consulta. Considerando a célula {Califórnia, T3, Custo da Loja} como S0, a soma inicial é i = 0 a 1. Para i = 0, a tupla ordinal no eixo 0 de {Custo da loja} é 1. Para i = 1, a tupla ordinal de {CA, T3} é 2.  
  
 Para i = 0, Ei = 1, então, para eu = 0 a soma é 1 * 1 = 1 e para eu = 1, a soma é 2 (tupla ordinal) vezes 4 (o valor de Ei calculado como 1 \* 4), ou 8. A soma de 1 + 8 é então 9, a célula ordinal para essa célula.  
  
## <a name="example"></a>Exemplo  
 O exemplo seguinte demonstra a estrutura do elemento `Cell`, incluindo os valores da propriedade VALUE, FORMATTED_VALUE, and FORMAT_STRING para cada célula.  
  
```  
<CellData>  
   <Cell CellOrdinal="0">  
      <Value xsi:type="xsd:double">16890</Value>  
      <FmtValue>16,890.00</FmtValue>  
      <FormatString>Standard</FormatString>  
   </Cell>  
   <Cell CellOrdinal="1">  
      <Value xsi:type="xsd:int">50</Value>  
      <FmtValue>50</FmtValue>  
      <FormatString>Standard</FormatString>  
   </Cell>  
   <Cell CellOrdinal="2">  
      <Value xsi:type="xsd:double">36175.2</Value>  
      <FmtValue>$36,175.20</FmtValue>  
      <FormatString>Currency</FormatString>  
   </Cell>  
</CellData>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de dados MDDataSet &#40;XMLA&#41;](../xml-data-types/mddataset-data-type-xmla.md)   
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
