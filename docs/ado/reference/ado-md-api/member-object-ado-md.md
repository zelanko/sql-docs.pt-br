---
title: O objeto de membro (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member
helpviewer_keywords:
- Member object [ADO MD], members
ms.assetid: 3dedf755-0741-4c3f-8b4e-bff8ff8809c8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 44d6b5f06bffb1cea786ba34d3d2aa8a3efb45ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949492"
---
# <a name="member-object-ado-md"></a>Objeto Member (ADO MD)
Representa um membro de um nível em um cubo, os filhos de um membro de um nível ou membro de uma posição ao longo do eixo de um conjunto de células.  
  
## <a name="remarks"></a>Comentários  
 As propriedades de um **membro** diferem, dependendo do contexto no qual ele é usado. Um **membro** de uma [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md) em um [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) tem uma [filhos](../../../ado/reference/ado-md-api/children-property-ado-md.md) propriedade que retorna o **membros** em o próximo nível inferior na hierarquia do atual **membro**. Para um **membro** de uma [posição](../../../ado/reference/ado-md-api/position-object-ado-md.md), o **filhos** coleção sempre está vazia. Além disso, o [tipo](../../../ado/reference/ado-md-api/type-property-ado-md.md) propriedade se aplica somente ao **membros** de um **nível**.  
  
 Um **membro** dos **posição** tem duas propriedades que são úteis ao exibir o [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md): [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md) e [ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md). Ocorrerá um erro se essas propriedades são acessadas em uma **membro** de uma **nível**.  
  
 Com as coleções e propriedades de um **membro** objeto de uma **nível**, você pode fazer o seguinte:  
  
-   Identificar o **membro** com o [nome](../../../ado/reference/ado-md-api/name-property-ado-md.md) e [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) propriedades.  
  
-   Retornar uma cadeia de caracteres a ser usado ao exibir o **membro** com o [legenda](../../../ado/reference/ado-md-api/caption-property-ado-md.md) propriedade.  
  
-   Retornar uma cadeia de caracteres significativa que descreve uma medida ou fórmula **membro** com o [descrição](../../../ado/reference/ado-md-api/description-property-ado-md.md) propriedade.  
  
-   Determinar a natureza do **membro** com o [tipo](../../../ado/reference/ado-md-api/type-property-ado-md.md) propriedade.  
  
-   Obter informações sobre o **nível** da **membro** com o [LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md) e [LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md) propriedades.  
  
-   Obter relacionados **membros** em um [hierarquia](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md) com o [pai](../../../ado/reference/ado-md-api/parent-property-ado-md.md) e [filhos](../../../ado/reference/ado-md-api/children-property-ado-md.md) propriedades.  
  
-   Contagem de filhos de um **membro** com o [ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md) propriedade.  
  
-   Use o padrão ADO [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção para obter informações adicionais sobre o **nível** objeto.  
  
 Com as coleções e propriedades de um **membro** de uma **posição** ao longo de um [eixo](../../../ado/reference/ado-md-api/axis-object-ado-md.md), você pode fazer o seguinte:  
  
-   Identificar o **membro** com o [nome](../../../ado/reference/ado-md-api/name-property-ado-md.md) e [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) propriedades.  
  
-   Retornar uma cadeia de caracteres a ser usado ao exibir o **membro** com o [legenda](../../../ado/reference/ado-md-api/caption-property-ado-md.md) propriedade.  
  
-   Retornar uma cadeia de caracteres significativa que descreve uma medida ou fórmula **membro** com o [descrição](../../../ado/reference/ado-md-api/description-property-ado-md.md) propriedade.  
  
-   Obter informações sobre o **nível** da **membro** com o [LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md) e [LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md) propriedades.  
  
-   Contagem de filhos de um **membro** com o [ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md) propriedade.  
  
-   Use o [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md) propriedade para determinar se há pelo menos um filho na **eixo** imediatamente após esta **membro**.  
  
-   Use o [ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md) propriedade para determinar se o pai deste **membro** é o mesmo que o pai do imediatamente anterior **membro**.  
  
-   Use o padrão ADO [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção para obter informações adicionais sobre o **nível** objeto.  
  
 O **propriedades** coleção contém propriedades fornecidos pelo provedor. A tabela a seguir lista as propriedades que podem estar disponíveis. A lista de propriedades reais pode diferir dependendo após a implementação do provedor. Consulte a documentação do seu provedor para obter uma lista completa de propriedades disponíveis.  
  
|Nome|Descrição|  
|----------|-----------------|  
|CatalogName|O nome do catálogo ao qual pertence este cubo.|  
|ChildrenCardinality|O número de filhos de um membro.|  
|CubeName|O nome do cubo.|  
|Descrição|Uma descrição significativa do membro.|  
|DimensionUniqueName|O nome ambíguo do [dimensão](../../../ado/reference/ado-md-api/dimension-object-ado-md.md).|  
|HierarchyUniqueName|O nome não ambíguo da hierarquia.|  
|LevelNumber|A distância entre o nível e a raiz da hierarquia.|  
|LevelUniqueName|O nome não ambíguo do nível.|  
|MemberCaption|Um rótulo ou legenda associado ao membro.|  
|MemberGUID|O GUID do membro.|  
|MemberName|O nome do membro.|  
|MemberOrdinal|O número ordinal do membro.|  
|MemberType|O tipo do membro.|  
|MemberUniqueName|O nome não ambíguo do membro.|  
|ParentCount|A contagem do número de pais deste membro.|  
|ParentLevel|O número do nível do pai do membro.|  
|ParentUniqueName|O nome não ambíguo do pai do membro.|  
|SchemaName|O nome do esquema ao qual pertence este cubo.|  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](../../../ado/reference/ado-md-api/member-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de catálogo (VB)](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [Coleção Members (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
