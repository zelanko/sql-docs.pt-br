---
title: Elemento PropertyList (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 49dad8f88ffb9fb517492ad7920ac1a260e1a912
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="propertylist-element-xmla"></a>Elemento PropertyList (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
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
  
## <a name="remarks"></a>Remarks  
 O elemento **PropertyList** contém uma coleção de propriedades XMLA. Cada propriedade permite ao usuário controlar alguns aspectos do método **Discover** ou **Execute** , como a definição de informações obrigatórias para estabelecer conexão com a fonte de dados, a especificação do formato de retorno do conjunto de resultados ou a especificação da localidade na qual os dados devem ser formatados. Cada propriedade XMLA no elemento **PropertyList** é definida por um elemento XML separado. O valor da propriedade XMLA são os dados contidos pelo elemento XML e o nome da propriedade XMLA que corresponde ao nome do elemento XML.  
  
 As propriedades disponíveis e seus valores podem ser obtidos usando o tipo de solicitação DISCOVER_PROPERTIES com o método **Discover** . Não há nenhum pedido obrigatório para as propriedades listadas no elemento **PropertyList** .  
  
 Para obter mais informações sobre as propriedades XMLA suportadas pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], consulte [propriedades com suporte do XMLA &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).  
  
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
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
