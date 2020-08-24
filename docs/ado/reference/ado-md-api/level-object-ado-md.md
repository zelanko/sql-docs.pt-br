---
description: Objeto Level (ADO MD)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3b77a0fad1b2ebe0f03855d9ff6c0ff689599774
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778045"
---
# <a name="level-object-ado-md"></a>Objeto Level (ADO MD)
Contém um conjunto de membros, cada um dos quais tem a mesma classificação em uma hierarquia.  
  
## <a name="remarks"></a>Comentários  
 Com as coleções e propriedades de um objeto de **nível** , você pode fazer o seguinte:  
  
-   Identifique o **nível** com as propriedades [Name](./name-property-ado-md.md) e [UniqueName](./uniquename-property-ado-md.md) .  
  
-   Retornar uma cadeia de caracteres a ser usada ao exibir o **nível** com a propriedade [Caption](./caption-property-ado-md.md) .  
  
-   Retorne uma cadeia de caracteres significativa que descreva o **nível** com a propriedade [Description](./description-property-ado-md.md) .  
  
-   Retornar os objetos de [membro](./member-object-ado-md.md) que compõem o **nível** com a coleção de [Membros](./members-collection-ado-md.md) .  
  
-   Retorna o número de níveis da raiz do **nível** com a propriedade [Depth](./depth-property-ado-md.md) .  
  
-   Use a coleção de [Propriedades](../ado-api/properties-collection-ado.md) padrão do ADO para obter informações adicionais sobre o objeto **Level** .  
  
 A coleção **Properties** contém propriedades fornecidas pelo provedor. A tabela a seguir lista as propriedades que podem estar disponíveis. A lista de propriedades real pode diferir dependendo da implementação do provedor. Consulte a documentação do seu provedor para obter uma lista mais completa das propriedades disponíveis.  
  
|Nome|Descrição|  
|----------|-----------------|  
|CatalogName|O nome do catálogo ao qual este cubo pertence.|  
|CubeName|O nome do cubo.|  
|Descrição|Uma descrição significativa do nível.|  
|DimensionUniqueName|O nome não ambíguo da [dimensão](./dimension-object-ado-md.md).|  
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
  
-   [Propriedades, métodos e eventos](./level-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de CubeDef (VBScript)](./cubedef-example-vbscript.md)   
 [Objeto Hierarchy (ADO MD)](./hierarchy-object-ado-md.md)   
 [Coleção de níveis (ADO MD)](./levels-collection-ado-md.md)   
 [Coleção Members (ADO MD)](./members-collection-ado-md.md)   
 [Coleção Properties (ADO)](../ado-api/properties-collection-ado.md)