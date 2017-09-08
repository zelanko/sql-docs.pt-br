---
title: Elemento PropertyList (XMLA) | Microsoft Docs
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
- PropertyList Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#PropertyList
- microsoft.xml.analysis.propertylist
- urn:schemas-microsoft-com:xml-analysis#PropertyList
helpviewer_keywords:
- PropertyList element
ms.assetid: 58e63bd9-8aac-438d-adba-1868b4d123f5
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d780b358d0d8d22ce5f71c5c90e87656a4cebee6
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="propertylist-element-xmla"></a>Elemento PropertyList (XMLA)
  Contém uma coleção de XML para propriedades de análise (XMLA) usadas pelo [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) e [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) métodos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Properties>  
   <PropertyList>  
      <!-- Zero or more XMLA properties -->  
   </PropertyList>  
</Properties>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Propriedades](../../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md)|  
|Elementos filho|Propriedades XMLA (consulte Comentários)|  
  
## <a name="remarks"></a>Comentários  
 O elemento **PropertyList** contém uma coleção de propriedades XMLA. Cada propriedade permite ao usuário controlar alguns aspectos do método **Discover** ou **Execute** , como a definição de informações obrigatórias para estabelecer conexão com a fonte de dados, a especificação do formato de retorno do conjunto de resultados ou a especificação da localidade na qual os dados devem ser formatados. Cada propriedade XMLA no elemento **PropertyList** é definida por um elemento XML separado. O valor da propriedade XMLA são os dados contidos pelo elemento XML e o nome da propriedade XMLA que corresponde ao nome do elemento XML.  
  
 As propriedades disponíveis e seus valores podem ser obtidos usando o tipo de solicitação DISCOVER_PROPERTIES com o método **Discover** . Não há nenhum pedido obrigatório para as propriedades listadas no elemento **PropertyList** .  
  
 Para obter mais informações sobre as propriedades XMLA suportadas pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], consulte [suporte para propriedades de XMLA &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).  
  
## <a name="example"></a>Exemplo  
  
```  
<Properties>  
   <PropertyList>  
      <DataSourceInfo>  
         Provider=MSOLAP;Data Source=local;  
      </DataSourceInfo>  
      <Catalog>  
         Foodmart 2000  
      </Catalog>  
      <Format>  
         Multidimensional  
      </Format>  
   </PropertyList>  
</Properties>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
