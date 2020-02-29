---
title: Membros (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- leaf members [Master Data Services]
- consolidated members [Master Data Services]
- consolidated members [Master Data Services], about consolidated members
- members [Master Data Services], about members
- leaf members [Master Data Services], about leaf members
- members [Master Data Services]
ms.assetid: 0fda32b9-677d-4ba2-bb28-f76f2383a30f
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 76b452e5ee362aeb2e66d8949a12ed910489f990
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175995"
---
# <a name="members-master-data-services"></a>Membros (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], os membros são os dados mestres físicos. Por exemplo, um membro pode ser uma Road-150 bike em uma entidade Product ou um cliente específico em uma entidade Customer.

## <a name="how-members-relate-to-other-model-objects"></a>Como os membros se relacionam com outros objetos modelo
 Você pode considerar os membros como linhas em uma tabela. Membros relacionados estão contidos em uma entidade e cada membro é definido por valores de atributos.

 Neste exemplo, a tabela representa uma entidade, as linhas da tabela representam membros e as colunas representam atributos. Cada célula representa um valor de atributo de um membro específico.

 ![Entidade de Master Data Services representada como tabela](../../2014/master-data-services/media/mds-conc-entity-table.gif "Entidade de Master Data Services representada como tabela")

## <a name="member-types"></a>Tipos de membro
 Há três tipos de membros: membros folha, membros consolidados e membros de coleção.

 Os membros folha são os membros padrão de uma entidade.

-   Em hierarquias derivadas, os membros folha são o único tipo de membro. Os membros folha de uma entidade são usados como pais dos membros folha de outra entidade.

-   Em hierarquias explícitas, os membros folha são o nível mais baixo e não podem ter filhos.

 Os membros consolidados existem apenas quando hierarquias e coleções explícitas são habilitadas para a entidade.

-   Hierarquias derivadas não contêm membros consolidados.

-   Em hierarquias explícitas, membros consolidados podem ser os pais de outros membros dentro da hierarquia ou podem ser filhos.

## <a name="use-hierarchies-and-collections-to-organize-members"></a>Usar hierarquias e coleções para organizar os membros
 As hierarquias e as coleções podem ser usadas para agrupar membros para relatório ou análise. Para obter mais informações, consulte [Hierarquias &#40;Master Data Services&#41;](hierarchies-master-data-services.md) e [Coleções &#40;Master Data Services&#41;](../../2014/master-data-services/collections-master-data-services.md).

## <a name="member-example"></a>Exemplo de membro
 No exemplo a seguir, cada membro é composto de um valor dos atributos Name, Code, Subcategory, StandardCost, ListPrice e FilePhoto.

 ![Tabela da entidade de produto bicicleta](../../2014/master-data-services/media/mds-conc-entity-table-w-data.gif "Tabela da entidade de produto bicicleta")

## <a name="related-tasks"></a>Related Tasks

|Descrição da tarefa|Tópico|
|----------------------|-----------|
|Criar um novo membro folha.|[Criar um membro folha &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-leaf-member-master-data-services.md)|
|Criar um novo membro consolidado.|[Criar um membro consolidado &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-consolidated-member-master-data-services.md)|
|Excluir um membro ou uma coleção existente.|[Excluir um membro ou uma coleção &#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-member-or-collection-master-data-services.md)|
|Reativar um membro ou coleção excluído.|[Reativar um membro ou uma coleção &#40;Master Data Services&#41;](../../2014/master-data-services/reactivate-a-member-or-collection-master-data-services.md)|
|Atualizar os valores de atributos de um membro.|[Altere o tipo de atributo &#40;Suplemento MDS para Excel&#41;](microsoft-excel-add-in/change-the-attribute-type-mds-add-in-for-excel.md)|
|Mover membros dentro de uma hierarquia.|[Mover membros dentro de uma hierarquia &#40;Master Data Services&#41;](../../2014/master-data-services/move-members-within-a-hierarchy-master-data-services.md)|

## <a name="related-content"></a>Conteúdo relacionado

-   [Visão geral do Master Data Services](master-data-services-overview-mds.md)

-   [Entidades &#40;Master Data Services&#41;](../../2014/master-data-services/entities-master-data-services.md)

-   [Atributos &#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)

-   [Hierarquias &#40;Master Data Services&#41;](hierarchies-master-data-services.md)

-   [Coleções &#40;Master Data Services&#41;](../../2014/master-data-services/collections-master-data-services.md)

-   [Permissões de folha &#40;Master Data Services&#41;](../../2014/master-data-services/leaf-permissions-master-data-services.md)

-   [Permissões consolidadas &#40;Master Data Services&#41;](../../2014/master-data-services/consolidated-permissions-master-data-services.md)

-   [Operadores de filtro &#40;Master Data Services&#41;](../../2014/master-data-services/filter-operators-master-data-services.md)


