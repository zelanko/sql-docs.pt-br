---
title: Nível de objeto (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level
helpviewer_keywords:
- Level object [ADO MD]
ms.assetid: 37815869-ed30-45fd-9aea-0a986c1b305c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e01d18edab653fd79a4b5122b8270d5b894feddd
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="level-object-ado-md"></a>Objeto de nível (ADO MD)
Contém um conjunto de membros, cada um deles tem a mesma classificação dentro de uma hierarquia.  
  
## <a name="remarks"></a>Remarks  
 Com as coleções e propriedades de um **nível** do objeto, você pode fazer o seguinte:  
  
-   Identificar o **nível** com o [nome](../../../ado/reference/ado-md-api/name-property-ado-md.md) e [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) propriedades.  
  
-   Retorna uma cadeia de caracteres a ser usado ao exibir o **nível** com o [legenda](../../../ado/reference/ado-md-api/caption-property-ado-md.md) propriedade.  
  
-   Retorna uma cadeia de caracteres significativa que descreve o **nível** com o [descrição](../../../ado/reference/ado-md-api/description-property-ado-md.md) propriedade.  
  
-   Retornar o [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) objetos que compõem o **nível** com o [membros](../../../ado/reference/ado-md-api/members-collection-ado-md.md) coleção.  
  
-   Retorna o número de níveis da raiz de **nível** com o [profundidade](../../../ado/reference/ado-md-api/depth-property-ado-md.md) propriedade.  
  
-   Usar o ADO padrão [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção para obter informações adicionais sobre o **nível** objeto.  
  
 O **propriedades** coleção contém propriedades fornecidos pelo provedor. A tabela a seguir lista as propriedades que podem estar disponíveis. A lista de propriedade real pode ser diferente dependendo da implementação do provedor. Consulte a documentação do provedor para obter uma lista mais completa de propriedades disponíveis.  
  
|Nome|Description|  
|----------|-----------------|  
|CatalogName|O nome do catálogo ao qual pertence este cubo.|  
|CubeName|O nome do cubo.|  
|Description|Uma descrição significativa do nível.|  
|DimensionUniqueName|O nome ambíguo do [dimensão](../../../ado/reference/ado-md-api/dimension-object-ado-md.md).|  
|HierarchyUniqueName|O nome ambíguo de hierarquia.|  
|LevelCaption|Um rótulo ou legenda associada ao nível.|  
|LevelCardinality|O número de membros no nível.|  
|LevelGUID|O GUID do nível.|  
|LevelName|Nome do nível.|  
|LevelNumber|A distância entre o nível e a raiz da hierarquia.|  
|LevelType|O tipo de nível.|  
|LevelUniqueName|O nome ambíguo do nível.|  
|SchemaName|O nome do esquema ao qual pertence este cubo.|  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](../../../ado/reference/ado-md-api/level-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de CubeDef (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Objeto de hierarquia (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)   
 [Coleção de níveis (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [Coleção de membros (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
