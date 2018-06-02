---
title: Elemento PropertyList (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3e773de16e65aa9c7f1be521214088aa9f06b369
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34577828"
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Propriedades](../../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md)|  
|Elementos filho|Propriedades XMLA (consulte Comentários)|  
  
## <a name="remarks"></a>Remarks  
 O elemento **PropertyList** contém uma coleção de propriedades XMLA. Cada propriedade permite ao usuário controlar alguns aspectos do método **Discover** ou **Execute** , como a definição de informações obrigatórias para estabelecer conexão com a fonte de dados, a especificação do formato de retorno do conjunto de resultados ou a especificação da localidade na qual os dados devem ser formatados. Cada propriedade XMLA no elemento **PropertyList** é definida por um elemento XML separado. O valor da propriedade XMLA são os dados contidos pelo elemento XML e o nome da propriedade XMLA que corresponde ao nome do elemento XML.  
  
 As propriedades disponíveis e seus valores podem ser obtidos usando o tipo de solicitação DISCOVER_PROPERTIES com o método **Discover** . Não há nenhum pedido obrigatório para as propriedades listadas no elemento **PropertyList** .  
  
 Para obter mais informações sobre as propriedades XMLA com suporte do Analysis Services, consulte [propriedades com suporte do XMLA &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).  
  
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
  
## <a name="see-also"></a>Confira também
 [Propriedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
