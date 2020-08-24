---
description: Objeto Member (ADO MD)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: c53b22dc0b5129fc822c4a012eefcf99041f5b45
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777995"
---
# <a name="member-object-ado-md"></a>Objeto Member (ADO MD)
Representa um membro de um nível em um cubo, os filhos de um membro de um nível ou um membro de uma posição ao longo de um eixo de um células.  
  
## <a name="remarks"></a>Comentários  
 As propriedades de um **membro** diferem dependendo do contexto no qual ele é usado. Um **membro** de um [nível](./level-object-ado-md.md) em um [CubeDef](./cubedef-object-ado-md.md) tem uma propriedade [Children](./children-property-ado-md.md) que retorna os **Membros** no próximo nível inferior na hierarquia do **membro**atual. Para um **membro** de uma [posição](./position-object-ado-md.md), a coleção de **filhos** está sempre vazia. Além disso, a propriedade [Type](./type-property-ado-md.md) aplica-se somente a **Membros** de um **nível**.  
  
 Um **membro** de **Position** tem duas propriedades que são úteis ao exibir [células](./cellset-object-ado-md.md): [DrilledDown](./drilleddown-property-ado-md.md) e [ParentSameAsPrev](./parentsameasprev-property-ado-md.md). Ocorrerá um erro se essas propriedades forem acessadas em um **membro** de um **nível**.  
  
 Com as coleções e propriedades de um objeto de **membro** de um **nível**, você pode fazer o seguinte:  
  
-   Identifique o **membro** com as propriedades [Name](./name-property-ado-md.md) e [UniqueName](./uniquename-property-ado-md.md) .  
  
-   Retornar uma cadeia de caracteres a ser usada ao exibir o **membro** com a propriedade [Caption](./caption-property-ado-md.md) .  
  
-   Retorne uma cadeia de caracteres significativa que descreve um **membro** de medida ou fórmula com a propriedade [Description](./description-property-ado-md.md) .  
  
-   Determine a natureza do **membro** com a propriedade [Type](./type-property-ado-md.md) .  
  
-   Obtenha informações sobre o **nível** do **membro** com as propriedades [LevelDepth](./leveldepth-property-ado-md.md) e [LevelName](./levelname-property-ado-md.md) .  
  
-   Obtenha **Membros** relacionados em uma [hierarquia](./hierarchy-object-ado-md.md) com as propriedades [pai](./parent-property-ado-md.md) e [filho](./children-property-ado-md.md) .  
  
-   Conte os filhos de um **membro** com a propriedade [ChildCount](./childcount-property-ado-md.md) .  
  
-   Use a coleção de [Propriedades](../ado-api/properties-collection-ado.md) padrão do ADO para obter informações adicionais sobre o objeto **Level** .  
  
 Com as coleções e propriedades de um **membro** de uma **posição** ao longo de um [eixo](./axis-object-ado-md.md), você pode fazer o seguinte:  
  
-   Identifique o **membro** com as propriedades [Name](./name-property-ado-md.md) e [UniqueName](./uniquename-property-ado-md.md) .  
  
-   Retornar uma cadeia de caracteres a ser usada ao exibir o **membro** com a propriedade [Caption](./caption-property-ado-md.md) .  
  
-   Retorne uma cadeia de caracteres significativa que descreve um **membro** de medida ou fórmula com a propriedade [Description](./description-property-ado-md.md) .  
  
-   Obtenha informações sobre o **nível** do **membro** com as propriedades [LevelDepth](./leveldepth-property-ado-md.md) e [LevelName](./levelname-property-ado-md.md) .  
  
-   Conte os filhos de um **membro** com a propriedade [ChildCount](./childcount-property-ado-md.md) .  
  
-   Use a propriedade [DrilledDown](./drilleddown-property-ado-md.md) para determinar se há pelo menos um filho no **eixo** imediatamente após este **membro**.  
  
-   Use a propriedade [ParentSameAsPrev](./parentsameasprev-property-ado-md.md) para determinar se o pai desse **membro** é o mesmo que o pai do **membro**imediatamente anterior.  
  
-   Use a coleção de [Propriedades](../ado-api/properties-collection-ado.md) padrão do ADO para obter informações adicionais sobre o objeto **Level** .  
  
 A coleção **Properties** contém propriedades fornecidas pelo provedor. A tabela a seguir lista as propriedades que podem estar disponíveis. A lista de propriedades real pode diferir dependendo da implementação do provedor. Consulte a documentação do seu provedor para obter uma lista mais completa das propriedades disponíveis.  
  
|Nome|Descrição|  
|----------|-----------------|  
|CatalogName|O nome do catálogo ao qual este cubo pertence.|  
|ChildrenCardinality|O número de filhos de um membro.|  
|CubeName|O nome do cubo.|  
|Descrição|Uma descrição significativa do membro.|  
|DimensionUniqueName|O nome não ambíguo da [dimensão](./dimension-object-ado-md.md).|  
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
  
-   [Propriedades, métodos e eventos](./member-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de catálogo (VB)](./catalog-example-vb.md)   
 [Coleção Members (ADO MD)](./members-collection-ado-md.md)   
 [Coleção Properties (ADO)](../ado-api/properties-collection-ado.md)