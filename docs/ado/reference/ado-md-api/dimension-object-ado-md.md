---
title: Objeto Dimension (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Dimension
helpviewer_keywords:
- Dimension object [ADO MD]
ms.assetid: 66adbbd2-23a3-4c19-a91b-84c31309aa1b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f7a13ad87d56f5e7855070d8fe577bb408d6ce9e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67938534"
---
# <a name="dimension-object-ado-md"></a>Objeto Dimension (ADO MD)
Representa uma das dimensões de um cubo multidimensional que contém uma ou mais hierarquias de membros.  
  
## <a name="remarks"></a>Comentários  
 Com as coleções e propriedades de um objeto **Dimension** , você pode fazer o seguinte:  
  
-   Identifique a **dimensão** com as propriedades [Name](../../../ado/reference/ado-md-api/name-property-ado-md.md) e [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) .  
  
-   Retorne uma cadeia de caracteres significativa que descreva a **dimensão** com a propriedade [Description](../../../ado/reference/ado-md-api/description-property-ado-md.md) .  
  
-   Retornar os objetos de [hierarquia](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md) que compõem a **dimensão** com a coleção de [hierarquias](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md) .  
  
-   Use a coleção de [Propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) padrão do ADO para obter informações adicionais sobre o objeto **Dimension** .  
  
 A coleção **Properties** contém propriedades fornecidas pelo provedor. A tabela a seguir lista as propriedades que podem estar disponíveis. A lista de propriedades real pode diferir dependendo da implementação do provedor. Consulte a documentação do seu provedor para obter uma lista mais completa das propriedades disponíveis.  
  
|Nome|DESCRIÇÃO|  
|----------|-----------------|  
|CatalogName|O nome do catálogo ao qual este cubo pertence.|  
|CubeName|O nome do cubo.|  
|DefaultHierarchy|O nome exclusivo da hierarquia padrão.|  
|DESCRIÇÃO|Uma descrição significativa do cubo.|  
|DimensionCaption|Um rótulo ou legenda associado à dimensão.|  
|DimensionCardinality|O número de membros na dimensão.|  
|DimensionGUID|O GUID da dimensão.|  
|DimensionName|O nome da dimensão.|  
|DimensionOrdinal|O número ordinal da dimensão entre o grupo de dimensões que formam o cubo.|  
|DimensionType|O tipo de dimensão.|  
|DimensionUniqueName|O nome não ambíguo da dimensão.|  
|SchemaName|O nome do esquema ao qual este cubo pertence.|  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](../../../ado/reference/ado-md-api/dimension-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de CubeDef (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Objeto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)   
 [Coleção Dimensions (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [Coleção de hierarquias (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
