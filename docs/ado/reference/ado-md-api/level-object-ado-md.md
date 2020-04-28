---
title: Objeto de nível (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level
helpviewer_keywords:
- Level object [ADO MD]
ms.assetid: 37815869-ed30-45fd-9aea-0a986c1b305c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4a44060ae4ffd9399c34d4cd8133f5ad7404ed5a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67949608"
---
# <a name="level-object-ado-md"></a>Objeto Level (ADO MD)
Contém um conjunto de membros, cada um dos quais tem a mesma classificação em uma hierarquia.  
  
## <a name="remarks"></a>Comentários  
 Com as coleções e propriedades de um objeto de **nível** , você pode fazer o seguinte:  
  
-   Identifique o **nível** com as propriedades [Name](../../../ado/reference/ado-md-api/name-property-ado-md.md) e [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) .  
  
-   Retornar uma cadeia de caracteres a ser usada ao exibir o **nível** com a propriedade [Caption](../../../ado/reference/ado-md-api/caption-property-ado-md.md) .  
  
-   Retorne uma cadeia de caracteres significativa que descreva o **nível** com a propriedade [Description](../../../ado/reference/ado-md-api/description-property-ado-md.md) .  
  
-   Retornar os objetos de [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) que compõem o **nível** com a coleção de [Membros](../../../ado/reference/ado-md-api/members-collection-ado-md.md) .  
  
-   Retorna o número de níveis da raiz do **nível** com a propriedade [Depth](../../../ado/reference/ado-md-api/depth-property-ado-md.md) .  
  
-   Use a coleção de [Propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) padrão do ADO para obter informações adicionais sobre o objeto **Level** .  
  
 A coleção **Properties** contém propriedades fornecidas pelo provedor. A tabela a seguir lista as propriedades que podem estar disponíveis. A lista de propriedades real pode diferir dependendo da implementação do provedor. Consulte a documentação do seu provedor para obter uma lista mais completa das propriedades disponíveis.  
  
|Nome|Descrição|  
|----------|-----------------|  
|CatalogName|O nome do catálogo ao qual este cubo pertence.|  
|CubeName|O nome do cubo.|  
|Descrição|Uma descrição significativa do nível.|  
|DimensionUniqueName|O nome não ambíguo da [dimensão](../../../ado/reference/ado-md-api/dimension-object-ado-md.md).|  
|HierarchyUniqueName|O nome não ambíguo da hierarquia.|  
|LevelCaption|Um rótulo ou legenda associado ao nível.|  
|LevelCardinality|O número de membros no nível.|  
|LevelGUID|O GUID do nível.|  
|LevelName|Nome do nível.|  
|LevelNumber|A distância entre o nível e a raiz da hierarquia.|  
|LevelType|O tipo de nível.|  
|LevelUniqueName|O nome não ambíguo do nível.|  
|SchemaName|O nome do esquema ao qual este cubo pertence.|  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](../../../ado/reference/ado-md-api/level-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de CubeDef (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Objeto Hierarchy (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)   
 [Coleção de níveis (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [Coleção Members (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
