---
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
ms.openlocfilehash: 1232d228d597188364cb20a7f60dfaa11c8af21a
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82753965"
---
# <a name="hierarchy-object-ado-md"></a>Objeto Hierarchy (ADO MD)
Representa uma maneira na qual os membros de uma [dimensão](../../../ado/reference/ado-md-api/dimension-object-ado-md.md) podem ser agregados ou "acumulados". Uma dimensão pode ser agregada ao longo de uma ou mais hierarquias.  
  
## <a name="remarks"></a>Comentários  
 Com as coleções e propriedades de um objeto de **hierarquia** , você pode fazer o seguinte:  
  
-   Identifique a **hierarquia** com as propriedades [Name](../../../ado/reference/ado-md-api/name-property-ado-md.md) e [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) .  
  
-   Retornar uma cadeia de caracteres significativa que descreve a **hierarquia** com a propriedade [Description](../../../ado/reference/ado-md-api/description-property-ado-md.md) .  
  
-   Retornar os objetos de [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md) que compõem a **hierarquia** com a coleção de [níveis](../../../ado/reference/ado-md-api/levels-collection-ado-md.md) .  
  
-   Use a coleção de [Propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) padrão do ADO para obter informações adicionais sobre o objeto **Hierarchy** .  
  
 A coleção **Properties** contém propriedades fornecidas pelo provedor. A tabela a seguir lista as propriedades que podem estar disponíveis. A lista de propriedades real pode diferir dependendo da implementação do provedor. Consulte a documentação do seu provedor para obter uma lista mais completa das propriedades disponíveis.  
  
|Name|Descrição|  
|----------|-----------------|  
|AllMember|O membro no nível mais alto de ROLLUP na hierarquia.|  
|CatalogName|O nome do catálogo ao qual este cubo pertence.|  
|CubeName|O nome do cubo.|  
|DefaultMember|O nome exclusivo do membro padrão para esta hierarquia.|  
|Description|Uma descrição significativa da hierarquia.|  
|DimensionType|O tipo de dimensão ao qual essa hierarquia pertence.|  
|DimensionUniqueName|O nome não ambíguo da dimensão.|  
|HierarchyCaption|Um rótulo ou legenda associada à hierarquia.|  
|HierarchyCardinality|O número de membros na hierarquia.|  
|HierarchyGUID|O GUID da hierarquia.|  
|HierarchyName|O nome da hierarquia.|  
|HierarchyUniqueName|O nome não ambíguo da hierarquia.|  
|SchemaName|O nome do esquema ao qual este cubo pertence.|  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](../../../ado/reference/ado-md-api/hierarchy-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de CubeDef (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Objeto Dimension (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [Coleção de hierarquias (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [Coleção de níveis (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
