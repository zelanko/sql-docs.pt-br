---
title: Membros (Master Data Services) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- leaf members [Master Data Services]
- consolidated members [Master Data Services]
- consolidated members [Master Data Services], about consolidated members
- members [Master Data Services], about members
- leaf members [Master Data Services], about leaf members
- members [Master Data Services]
ms.assetid: 0fda32b9-677d-4ba2-bb28-f76f2383a30f
caps.latest.revision: "16"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 092d0f9ca2dfd5bb477573b7db85634930c8c435
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="members-master-data-services"></a>Membros (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], os membros são os dados mestres físicos. Por exemplo, um membro pode ser uma Road-150 bike em uma entidade Product ou um cliente específico em uma entidade Customer.  
  
## <a name="how-members-relate-to-other-model-objects"></a>Como os membros se relacionam com outros objetos modelo  
 Você pode considerar os membros como linhas em uma tabela. Membros relacionados estão contidos em uma entidade e cada membro é definido por valores de atributos.  
  
 Neste exemplo, a tabela representa uma entidade, as linhas da tabela representam membros e as colunas representam atributos. Cada célula representa um valor de atributo de um membro específico.  
  
 ![Entidade do Master Data Services representada como tabela](../master-data-services/media/mds-conc-entity-table.gif "Entidade do Master Data Services representada como tabela")  
  
## <a name="member-types"></a>Tipos de membro  
 Há três tipos de membros: membros folha, membros consolidados e membros de coleção.  
  
 Os membros folha são os membros padrão de uma entidade.  
  
-   Em hierarquias derivadas, os membros folha são o único tipo de membro. Os membros folha de uma entidade são usados como pais dos membros folha de outra entidade.  
  
-   Em hierarquias explícitas, os membros folha são o nível mais baixo e não podem ter filhos.  
  
 Os membros consolidados existem apenas quando hierarquias e coleções explícitas são habilitadas para a entidade.  
  
-   Hierarquias derivadas não contêm membros consolidados.  
  
-   Em hierarquias explícitas, membros consolidados podem ser os pais de outros membros dentro da hierarquia ou podem ser filhos.  
  
## <a name="use-hierarchies-and-collections-to-organize-members"></a>Usar hierarquias e coleções para organizar os membros  
 As hierarquias e as coleções podem ser usadas para agrupar membros para relatório ou análise. Para obter mais informações, consulte [Hierarquias &#40;Master Data Services&#41;](../master-data-services/hierarchies-master-data-services.md) e [Coleções &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md).  
  
## <a name="member-example"></a>Exemplo de membro  
 No exemplo a seguir, cada membro é composto de um valor dos atributos Name, Code, Subcategory, StandardCost, ListPrice e FilePhoto.  
  
 ![Tabela de entidade de produto de bicicleta](../master-data-services/media/mds-conc-entity-table-w-data.gif "Tabela de entidade de produto de bicicleta")  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Criar um novo membro folha.|[Criar um membro folha &#40;Master Data Services&#41;](../master-data-services/create-a-leaf-member-master-data-services.md)|  
|Criar um novo membro consolidado.|[Criar um membro consolidado &#40;Master Data Services&#41;](../master-data-services/create-a-consolidated-member-master-data-services.md)|  
|Excluir um membro ou uma coleção existente.|[Excluir um membro ou uma coleção &#40;Master Data Services&#41;](../master-data-services/delete-a-member-or-collection-master-data-services.md)|  
|Reativar um membro ou coleção excluído.|[Reativar um membro ou uma coleção &#40;Master Data Services&#41;](../master-data-services/reactivate-a-member-or-collection-master-data-services.md)|  
|Atualizar os valores de atributos de um membro.|[Alterar o tipo de atributo &#40;Suplemento MDS para Excel&#41;](../master-data-services/microsoft-excel-add-in/change-the-attribute-type-mds-add-in-for-excel.md)|  

  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Visão geral do Master Data Services &#40;MDS&#41;](../master-data-services/master-data-services-overview-mds.md)  
  
-   [Entidades &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)  
  
-   [Atributos &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
-   [Hierarquias &#40;Master Data Services&#41;](../master-data-services/hierarchies-master-data-services.md)  
  
-   [Coleções &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)  
  
-   [Permissões de folha &#40;Master Data Services&#41;](../master-data-services/leaf-permissions-master-data-services.md)  
  
 
-   [Operadores de filtro &#40;Master Data Services&#41;](../master-data-services/filter-operators-master-data-services.md)  
  
  
