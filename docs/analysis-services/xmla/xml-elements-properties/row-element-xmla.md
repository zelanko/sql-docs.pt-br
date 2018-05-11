---
title: Elemento Row (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 78745ed581642092c17190c4b81eb3f9ab6df853
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="row-element-xmla"></a>Elemento row (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contém uma única linha de dados para um elemento [root](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) que contém dados tabulares retornados por uma chamada do método [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) ou [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">  
   <row>  
      <!-- One or more column elements -->  
   </row>  
</root>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[root](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) (usando o tipo de dados [Rowset](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md) )|  
|Elementos filho|Um ou mais elementos de coluna.|  
  
## <a name="remarks"></a>Remarks  
 Cada linha retornada por um elemento **root** que contém dados tabulares tem um elemento **row** correspondente. Cada coluna no elemento **root** é representada por um elemento XML separado. O valor da coluna para o elemento **row** equivale aos dados contidos pelo elemento XML e o nome da coluna corresponde ao nome do elemento XML.  
  
 Há dois modos para expressar um valor nulo para uma coluna em uma linha:  
  
-   Um elemento de coluna ausente indica que a coluna é nula.  
  
-   O elemento de coluna pode usar o atributo `xsi:nil='true'` para indicar que tem um valor nulo.  
  
 Por exemplo, se uma linha tiver uma única coluna chamada Store_Name e seu valor for NULL, ela poderá ser representada como:  
  
```  
<row>  
</row>  
```  
  
 Ou:  
  
```  
<row>  
   <Store_name xsi:nil='true'/>  
</row>  
```  
  
 Se um elemento de coluna contiver um erro, um elemento **Error** fornecerá informações sobre o erro, conforme descrito no exemplo a seguir:  
  
```  
<row>   <Store_name>  
      <Error xmlns="urn:schemas-microsoft-com:xml-analysis:exception">  
         <ErrorCode>3238658054</ErrorCode>  
         <Description>The object [X] was not found in the cube when [X] was parsed.</Description>  
      </Error>  
   </Store_name>  
</row>  
```  
  
 Para obter mais informações sobre nomes de coluna e informações de esquema para dados de tabela, consulte [tipo de dados do conjunto de linhas & #40; XMLA & #41; ](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
