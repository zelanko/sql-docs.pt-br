---
description: Objeto Hierarchy (ADO MD)
title: Objeto Hierarchy (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Hierarchy
helpviewer_keywords:
- Hierarchy object [ADO MD]
ms.assetid: 034af340-ac79-494e-ba5e-2b57da1cb9de
author: rothja
ms.author: jroth
ms.openlocfilehash: fe14e37829bbeb501debcf1e8a27bd86d43712d3
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778085"
---
# <a name="hierarchy-object-ado-md"></a>Objeto Hierarchy (ADO MD)
Representa uma maneira na qual os membros de uma [dimensão](./dimension-object-ado-md.md) podem ser agregados ou "acumulados". Uma dimensão pode ser agregada ao longo de uma ou mais hierarquias.  
  
## <a name="remarks"></a>Comentários  
 Com as coleções e propriedades de um objeto de **hierarquia** , você pode fazer o seguinte:  
  
-   Identifique a **hierarquia** com as propriedades [Name](./name-property-ado-md.md) e [UniqueName](./uniquename-property-ado-md.md) .  
  
-   Retornar uma cadeia de caracteres significativa que descreve a **hierarquia** com a propriedade [Description](./description-property-ado-md.md) .  
  
-   Retornar os objetos de [nível](./level-object-ado-md.md) que compõem a **hierarquia** com a coleção de [níveis](./levels-collection-ado-md.md) .  
  
-   Use a coleção de [Propriedades](../ado-api/properties-collection-ado.md) padrão do ADO para obter informações adicionais sobre o objeto **Hierarchy** .  
  
 A coleção **Properties** contém propriedades fornecidas pelo provedor. A tabela a seguir lista as propriedades que podem estar disponíveis. A lista de propriedades real pode diferir dependendo da implementação do provedor. Consulte a documentação do seu provedor para obter uma lista mais completa das propriedades disponíveis.  
  
|Nome|Descrição|  
|----------|-----------------|  
|AllMember|O membro no nível mais alto de ROLLUP na hierarquia.|  
|CatalogName|O nome do catálogo ao qual este cubo pertence.|  
|CubeName|O nome do cubo.|  
|DefaultMember|O nome exclusivo do membro padrão para esta hierarquia.|  
|Descrição|Uma descrição significativa da hierarquia.|  
|DimensionType|O tipo de dimensão ao qual essa hierarquia pertence.|  
|DimensionUniqueName|O nome não ambíguo da dimensão.|  
|HierarchyCaption|Um rótulo ou legenda associada à hierarquia.|  
|HierarchyCardinality|O número de membros na hierarquia.|  
|HierarchyGUID|O GUID da hierarquia.|  
|HierarchyName|O nome da hierarquia.|  
|HierarchyUniqueName|O nome não ambíguo da hierarquia.|  
|SchemaName|O nome do esquema ao qual este cubo pertence.|  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](./hierarchy-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de CubeDef (VBScript)](./cubedef-example-vbscript.md)   
 [Objeto Dimension (ADO MD)](./dimension-object-ado-md.md)   
 [Coleção de hierarquias (ADO MD)](./hierarchies-collection-ado-md.md)   
 [Coleção de níveis (ADO MD)](./levels-collection-ado-md.md)   
 [Coleção Properties (ADO)](../ado-api/properties-collection-ado.md)