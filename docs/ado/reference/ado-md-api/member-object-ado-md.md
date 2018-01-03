---
title: Membro de objeto (ADO MD) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Member
helpviewer_keywords: Member object [ADO MD], members
ms.assetid: 3dedf755-0741-4c3f-8b4e-bff8ff8809c8
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6624e44343ef680c317338ea1fe32ead2aa0d9d0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="member-object-ado-md"></a>Membro de objeto (ADO MD)
Representa um membro de um nível em um cubo, os filhos de um membro de um nível ou membro de uma posição em um eixo de um conjunto de células.  
  
## <a name="remarks"></a>Remarks  
 As propriedades de um **membro** diferem dependendo do contexto no qual ele é usado. Um **membro** de um [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md) em uma [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) tem um [filhos](../../../ado/reference/ado-md-api/children-property-ado-md.md) propriedade retorna o **membros** em o próximo nível inferior na hierarquia da atual **membro**. Para uma **membro** de um [posição](../../../ado/reference/ado-md-api/position-object-ado-md.md), o **filhos** coleção sempre está vazia. Além disso, o [tipo](../../../ado/reference/ado-md-api/type-property-ado-md.md) propriedade se aplica somente ao **membros** de um **nível**.  
  
 Um **membro** de **posição** tem duas propriedades que são úteis ao exibir o [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md): [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md) e [ ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md). Ocorrerá um erro se essas propriedades são acessadas em uma **membro** de um **nível**.  
  
 Com as coleções e propriedades de um **membro** objeto de um **nível**, você pode fazer o seguinte:  
  
-   Identificar o **membro** com o [nome](../../../ado/reference/ado-md-api/name-property-ado-md.md) e [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) propriedades.  
  
-   Retorna uma cadeia de caracteres a ser usado ao exibir o **membro** com o [legenda](../../../ado/reference/ado-md-api/caption-property-ado-md.md) propriedade.  
  
-   Retornar uma cadeia de caracteres significativa que descreve uma fórmula ou medida **membro** com o [descrição](../../../ado/reference/ado-md-api/description-property-ado-md.md) propriedade.  
  
-   Determinar a natureza do **membro** com o [tipo](../../../ado/reference/ado-md-api/type-property-ado-md.md) propriedade.  
  
-   Obter informações sobre o **nível** do **membro** com o [LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md) e [LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md) propriedades.  
  
-   Obter relacionados **membros** em uma [hierarquia](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md) com o [pai](../../../ado/reference/ado-md-api/parent-property-ado-md.md) e [filhos](../../../ado/reference/ado-md-api/children-property-ado-md.md) propriedades.  
  
-   Contagem de filhos de um **membro** com o [ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md) propriedade.  
  
-   Usar o ADO padrão [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção para obter informações adicionais sobre o **nível** objeto.  
  
 Com as coleções e propriedades de um **membro** de um **posição** ao longo de um [eixo](../../../ado/reference/ado-md-api/axis-object-ado-md.md), você pode fazer o seguinte:  
  
-   Identificar o **membro** com o [nome](../../../ado/reference/ado-md-api/name-property-ado-md.md) e [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) propriedades.  
  
-   Retorna uma cadeia de caracteres a ser usado ao exibir o **membro** com o [legenda](../../../ado/reference/ado-md-api/caption-property-ado-md.md) propriedade.  
  
-   Retornar uma cadeia de caracteres significativa que descreve uma fórmula ou medida **membro** com o [descrição](../../../ado/reference/ado-md-api/description-property-ado-md.md) propriedade.  
  
-   Obter informações sobre o **nível** do **membro** com o [LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md) e [LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md) propriedades.  
  
-   Contagem de filhos de um **membro** com o [ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md) propriedade.  
  
-   Use o [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md) propriedade para determinar se há pelo menos um filho no **eixo** imediatamente após isso **membro**.  
  
-   Use o [ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md) propriedade para determinar se o pai desta **membro** é o mesmo que o pai do imediatamente anterior **membro**.  
  
-   Usar o ADO padrão [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção para obter informações adicionais sobre o **nível** objeto.  
  
 O **propriedades** coleção contém propriedades fornecidos pelo provedor. A tabela a seguir lista as propriedades que podem estar disponíveis. A lista de propriedade real pode ser diferente dependendo da implementação do provedor. Consulte a documentação do provedor para obter uma lista mais completa de propriedades disponíveis.  
  
|Nome|Description|  
|----------|-----------------|  
|CatalogName|O nome do catálogo ao qual pertence este cubo.|  
|ChildrenCardinality|O número de filhos de um membro.|  
|CubeName|O nome do cubo.|  
|Description|Uma descrição significativa do membro.|  
|DimensionUniqueName|O nome ambíguo do [dimensão](../../../ado/reference/ado-md-api/dimension-object-ado-md.md).|  
|HierarchyUniqueName|O nome ambíguo de hierarquia.|  
|LevelNumber|A distância entre o nível e a raiz da hierarquia.|  
|LevelUniqueName|O nome ambíguo do nível.|  
|MemberCaption|Um rótulo ou legenda associado ao membro.|  
|MemberGUID|O GUID do membro.|  
|MemberName|O nome do membro.|  
|MemberOrdinal|O número ordinal do membro.|  
|MemberType|O tipo do membro.|  
|MemberUniqueName|O nome ambíguo do membro.|  
|ParentCount|A contagem do número de pais deste membro.|  
|ParentLevel|O número do nível do pai do membro.|  
|ParentUniqueName|O nome ambíguo do pai do membro.|  
|SchemaName|O nome do esquema ao qual pertence este cubo.|  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](../../../ado/reference/ado-md-api/member-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de catálogo (VB)](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [Coleção de membros (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
