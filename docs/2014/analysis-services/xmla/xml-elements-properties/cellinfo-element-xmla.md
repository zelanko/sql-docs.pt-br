---
title: Elemento CellInfo (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CellInfo Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.cellinfo
- http://schemas.microsoft.com/analysisservices/2003/engine#CellInfo
- urn:schemas-microsoft-com:xml-analysis#CellInfo
helpviewer_keywords:
- CellInfo element
ms.assetid: 8b6420f1-e9a7-4975-b580-1439fa11f5ca
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 693495e50c78760cd130df6d12f359d96c5c0807
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48216488"
---
# <a name="cellinfo-element-xmla"></a>Elemento CellInfo (XMLA)
  Representa os metadados de célula contidos pelo pai [OlapInfo](olapinfo-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<OlapInfo>  
   ...  
   <CellInfo>  
      <!-- One or more cell property definitions -->  
   </CellInfo>  
   ...  
</OlapInfo>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|None|  
|Valor padrão|None|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[OlapInfo](olapinfo-element-xmla.md)|  
|Elementos filho|Uma ou mais definições de propriedade de célula|  
  
## <a name="remarks"></a>Comentários  
 O elemento `CellInfo` contém uma coleção de propriedades de célula para as células incluídas no conjunto de dados multidimensionais retornado por um elemento `root` usando o tipo de dados `MDDataSet`. Cada propriedade de célula no elemento `CellInfo` é definida por um elemento XML separado, cada um com um atributo `name` e um atributo `type`. O atributo `name` da propriedade de célula corresponde ao nome do comando OLE DB para a propriedade de célula OLAP representada pelo elemento XML e o atributo `type` representa o tipo de dados XML da propriedade de célula. O nome do elemento XML é usado para identificar o valor da propriedade de célula para as células contidas no elemento `CellData` do elemento `root`.  
  
 A sintaxe a seguir descreve uma definição de propriedade de célula:  
  
```  
<CellPropertyDefinition name="string" type"string" />  
```  
  
 As propriedades disponíveis e seus valores podem ser obtidos usando o tipo de solicitação DISCOVER_PROPERTIES com o `Discover` método. Não há nenhum pedido obrigatório para as propriedades listadas no elemento `PropertyList`.  
  
 Um provedor pode especificar valores padrão opcionalmente para propriedades de célula ou membros individuais na seção `AxisInfo` ou `CellInfo`. Os valores padrão podem fornecer um resultado menor se a propriedade sempre ou quase sempre tiver o mesmo valor. Para indicar um valor padrão para uma propriedade, o`Default` elemento pode ser especificado opcionalmente como um elemento filho de um dos elementos de definição de propriedade da célula. Portanto, a ausência de um membro ou propriedade de célula no resultado indica que o padrão declarado é o valor da propriedade de célula.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como as propriedades de célula VALUE, FORMATTED_VALUE e FORMAT_STRING são representadas no elemento `CellInfo`.  
  
```  
<OlapInfo>  
   ...  
      <CellInfo>  
         <Value name="VALUE"></Value>  
         <FmtValue name="FORMATTED_VALUE"></FmtValue>  
         <FormatString name="FORMAT_STRING"></FormatString>  
      </CellInfo>  
</OlapInfo>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
