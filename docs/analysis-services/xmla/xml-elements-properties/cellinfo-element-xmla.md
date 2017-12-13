---
title: Elemento CellInfo (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
apiname: CellInfo Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.cellinfo
- http://schemas.microsoft.com/analysisservices/2003/engine#CellInfo
- urn:schemas-microsoft-com:xml-analysis#CellInfo
helpviewer_keywords: CellInfo element
ms.assetid: 8b6420f1-e9a7-4975-b580-1439fa11f5ca
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6f3d572ebdc461a5323d4e2675d23137063ff307
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="cellinfo-element-xmla"></a>Elemento CellInfo (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Representa os metadados de célula contidos pelo pai [OlapInfo](../../../analysis-services/xmla/xml-elements-properties/olapinfo-element-xmla.md) elemento.  
  
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[OlapInfo](../../../analysis-services/xmla/xml-elements-properties/olapinfo-element-xmla.md)|  
|Elementos filho|Uma ou mais definições de propriedade de célula|  
  
## <a name="remarks"></a>Comentários  
 O **CellInfo** elemento contém uma coleção de propriedades de célula para as células incluídas no conjunto de dados multidimensional retornado por uma **raiz** elemento usando o **MDDataSet**tipo de dados. Cada propriedade de célula no **CellInfo** elemento é definido por um elemento XML separado, cada um com um **nome** atributo e um **tipo** atributo. O **nome** atributo da propriedade de célula corresponde ao nome do OLE DB para a propriedade de célula OLAP representada pelo elemento XML e o **tipo** atributo representa o tipo de dados XML da célula propriedade. O nome do elemento XML é usado para identificar o valor da propriedade de célula para as células contidas no **CellData** elemento o **raiz** elemento.  
  
 A sintaxe a seguir descreve uma definição de propriedade de célula:  
  
```  
<CellPropertyDefinition name="string" type"string" />  
```  
  
 As propriedades disponíveis e seus valores podem ser obtidos usando o tipo de solicitação DISCOVER_PROPERTIES com o método **Discover** . Não há nenhum pedido obrigatório para as propriedades listadas no elemento **PropertyList** .  
  
 Um provedor pode opcionalmente especificar valores padrão para propriedades de célula ou membros individuais no **AxisInfo** ou **CellInfo** seção. Os valores padrão podem fornecer um resultado menor se a propriedade sempre ou quase sempre tiver o mesmo valor. Para indicar um valor padrão para uma propriedade, o**padrão** elemento pode ser especificado opcionalmente como um elemento filho de um dos elementos de definição de propriedade de célula. Portanto, a ausência de um membro ou propriedade de célula no resultado indica que o padrão declarado é o valor da propriedade de célula.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como as propriedades de célula de valor, FORMATTED_VALUE e FORMAT_STRING são representadas no **CellInfo** elemento.  
  
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
 [Propriedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
