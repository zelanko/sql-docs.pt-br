---
title: Objeto member (ADO MD) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949492"
---
# <a name="member-object-ado-md"></a>Objeto Member (ADO MD)
Representa um membro de um nível em um cubo, os filhos de um membro de um nível ou um membro de uma posição ao longo de um eixo de um células.  
  
## <a name="remarks"></a>Comentários  
 As propriedades de um **membro** diferem dependendo do contexto no qual ele é usado. Um **membro** de um [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md) em um [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) tem uma propriedade [Children](../../../ado/reference/ado-md-api/children-property-ado-md.md) que retorna os **Membros** no próximo nível inferior na hierarquia do **membro**atual. Para um **membro** de uma [posição](../../../ado/reference/ado-md-api/position-object-ado-md.md), a coleção de **filhos** está sempre vazia. Além disso, a propriedade [Type](../../../ado/reference/ado-md-api/type-property-ado-md.md) aplica-se somente a **Membros** de um **nível**.  
  
 Um **membro** de **Position** tem duas propriedades que são úteis ao exibir [células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md): [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md) e [ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md). Ocorrerá um erro se essas propriedades forem acessadas em um **membro** de um **nível**.  
  
 Com as coleções e propriedades de um objeto de **membro** de um **nível**, você pode fazer o seguinte:  
  
-   Identifique o **membro** com as propriedades [Name](../../../ado/reference/ado-md-api/name-property-ado-md.md) e [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) .  
  
-   Retornar uma cadeia de caracteres a ser usada ao exibir o **membro** com a propriedade [Caption](../../../ado/reference/ado-md-api/caption-property-ado-md.md) .  
  
-   Retorne uma cadeia de caracteres significativa que descreve um **membro** de medida ou fórmula com a propriedade [Description](../../../ado/reference/ado-md-api/description-property-ado-md.md) .  
  
-   Determine a natureza do **membro** com a propriedade [Type](../../../ado/reference/ado-md-api/type-property-ado-md.md) .  
  
-   Obtenha informações sobre o **nível** do **membro** com as propriedades [LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md) e [LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md) .  
  
-   Obtenha **Membros** relacionados em uma [hierarquia](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md) com as propriedades [pai](../../../ado/reference/ado-md-api/parent-property-ado-md.md) e [filho](../../../ado/reference/ado-md-api/children-property-ado-md.md) .  
  
-   Conte os filhos de um **membro** com a propriedade [ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md) .  
  
-   Use a coleção de [Propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) padrão do ADO para obter informações adicionais sobre o objeto **Level** .  
  
 Com as coleções e propriedades de um **membro** de uma **posição** ao longo de um [eixo](../../../ado/reference/ado-md-api/axis-object-ado-md.md), você pode fazer o seguinte:  
  
-   Identifique o **membro** com as propriedades [Name](../../../ado/reference/ado-md-api/name-property-ado-md.md) e [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) .  
  
-   Retornar uma cadeia de caracteres a ser usada ao exibir o **membro** com a propriedade [Caption](../../../ado/reference/ado-md-api/caption-property-ado-md.md) .  
  
-   Retorne uma cadeia de caracteres significativa que descreve um **membro** de medida ou fórmula com a propriedade [Description](../../../ado/reference/ado-md-api/description-property-ado-md.md) .  
  
-   Obtenha informações sobre o **nível** do **membro** com as propriedades [LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md) e [LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md) .  
  
-   Conte os filhos de um **membro** com a propriedade [ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md) .  
  
-   Use a propriedade [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md) para determinar se há pelo menos um filho no **eixo** imediatamente após este **membro**.  
  
-   Use a propriedade [ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md) para determinar se o pai desse **membro** é o mesmo que o pai do **membro**imediatamente anterior.  
  
-   Use a coleção de [Propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) padrão do ADO para obter informações adicionais sobre o objeto **Level** .  
  
 A coleção **Properties** contém propriedades fornecidas pelo provedor. A tabela a seguir lista as propriedades que podem estar disponíveis. A lista de propriedades real pode diferir dependendo da implementação do provedor. Consulte a documentação do seu provedor para obter uma lista mais completa das propriedades disponíveis.  
  
|Nome|DESCRIÇÃO|  
|----------|-----------------|  
|CatalogName|O nome do catálogo ao qual este cubo pertence.|  
|ChildrenCardinality|O número de filhos de um membro.|  
|CubeName|O nome do cubo.|  
|DESCRIÇÃO|Uma descrição significativa do membro.|  
|DimensionUniqueName|O nome não ambíguo da [dimensão](../../../ado/reference/ado-md-api/dimension-object-ado-md.md).|  
|HierarchyUniqueName|O nome não ambíguo da hierarquia.|  
|LevelNumber|A distância entre o nível e a raiz da hierarquia.|  
|LevelUniqueName|O nome não ambíguo do nível.|  
|MemberCaption|Um rótulo ou legenda associado ao membro.|  
|MemberGUID|O GUID do membro.|  
|MemberName|O nome do membro.|  
|MemberOrdinal|O número ordinal do membro.|  
|MemberType|O tipo do membro.|  
|MemberUniqueName|O nome não ambíguo do membro.|  
|ParentCount|A contagem do número de pais que esse membro tem.|  
|ParentLevel|O número de nível do pai do membro.|  
|ParentUniqueName|O nome não ambíguo do pai do membro.|  
|SchemaName|O nome do esquema ao qual este cubo pertence.|  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](../../../ado/reference/ado-md-api/member-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de catálogo (VB)](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [Coleção Members (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
