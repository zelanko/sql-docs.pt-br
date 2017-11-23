---
title: Objeto de hierarquia (ADO MD) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Hierarchy
helpviewer_keywords: Hierarchy object [ADO MD]
ms.assetid: 034af340-ac79-494e-ba5e-2b57da1cb9de
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e02aefb90af923cea7bfd6d33b8b1e97415c6ae8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="hierarchy-object-ado-md"></a>Objeto de hierarquia (ADO MD)
Representa uma forma em que os membros de um [dimensão](../../../ado/reference/ado-md-api/dimension-object-ado-md.md) podem ser agregados ou "acumulados". Uma dimensão pode ser agregada a uma ou mais hierarquias.  
  
## <a name="remarks"></a>Comentários  
 Com as coleções e propriedades de um **hierarquia** do objeto, você pode fazer o seguinte:  
  
-   Identificar o **hierarquia** com o [nome](../../../ado/reference/ado-md-api/name-property-ado-md.md) e [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) propriedades.  
  
-   Retorna uma cadeia de caracteres significativa que descreve o **hierarquia** com o [descrição](../../../ado/reference/ado-md-api/description-property-ado-md.md) propriedade.  
  
-   Retornar o [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md) objetos que compõem o **hierarquia** com o [níveis](../../../ado/reference/ado-md-api/levels-collection-ado-md.md) coleção.  
  
-   Usar o ADO padrão [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção para obter informações adicionais sobre o **hierarquia** objeto.  
  
 O **propriedades** coleção contém propriedades fornecidos pelo provedor. A tabela a seguir lista as propriedades que podem estar disponíveis. A lista de propriedade real pode ser diferente dependendo da implementação do provedor. Consulte a documentação do provedor para obter uma lista mais completa de propriedades disponíveis.  
  
|Nome|Description|  
|----------|-----------------|  
|AllMember|O membro no nível mais alto do rollup na hierarquia.|  
|CatalogName|O nome do catálogo ao qual pertence este cubo.|  
|CubeName|O nome do cubo.|  
|DefaultMember|O nome exclusivo do membro padrão para essa hierarquia.|  
|Description|Uma descrição significativa da hierarquia.|  
|DimensionType|O tipo de dimensão à qual pertence essa hierarquia.|  
|DimensionUniqueName|O nome ambíguo de dimensão.|  
|HierarchyCaption|Um rótulo ou legenda associada à hierarquia.|  
|HierarchyCardinality|O número de membros na hierarquia.|  
|HierarchyGUID|O GUID da hierarquia.|  
|HierarchyName|O nome da hierarquia.|  
|HierarchyUniqueName|O nome ambíguo de hierarquia.|  
|SchemaName|O nome do esquema ao qual pertence este cubo.|  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](../../../ado/reference/ado-md-api/hierarchy-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de CubeDef (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Objeto de dimensão (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [Coleção hierarquias (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [Coleção de níveis (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
