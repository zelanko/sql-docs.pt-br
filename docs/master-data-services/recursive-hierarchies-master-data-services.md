---
title: Hierarquias recursivas (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- recursive hierarchies [Master Data Services]
- hierarchies [Master Data Services], recursive hierarchies
ms.assetid: 9408c6ea-d9c4-4a0b-8a1b-1457fb6944af
caps.latest.revision: 8
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0afab3686ee2223d0902b59352274cc974cd49cb
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="recursive-hierarchies-master-data-services"></a>Hierarquias recursivas (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], uma hierarquia recursiva é uma hierarquia derivada que inclui uma relação recursiva. Uma relação recursiva existe quando uma entidade tem um atributo baseado em domínio com base na própria entidade.  
  
## <a name="recursive-hierarchy-example"></a>Exemplo de hierarquia recursiva  
 Um exemplo típico de hierarquia recursiva é uma estrutura organizacional. No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], você pode fazer isso criando uma entidade Funcionário com um atributo baseado em domínio chamado Gerente. O atributo Gerente é populado da lista de funcionários. Nesta organização de exemplo, todos os funcionários podem ser gerentes.  
  
 ![mds_conc_recursive_table_w_data](../master-data-services/media/mds-conc-recursive-table-w-data.gif "mds_conc_recursive_table_w_data")  
  
 Você pode criar uma hierarquia derivada que destaca a relação entre a entidade Funcionário e o atributo Gerente baseado em domínio.  
  
 ![mds_conc_recursive_UI_structure](../master-data-services/media/mds-conc-recursive-ui-structure.gif "mds_conc_recursive_UI_structure")  
  
 Para incluir cada membro na hierarquia apenas uma vez, você pode ancorar relações nulas. Quando você fizer isso, os membros com valores de atributo baseado em domínio em branco serão exibidos no nível superior da hierarquia.  
  
 ![mds_conc_recursive_UI_example_anchored](../master-data-services/media/mds-conc-recursive-ui-example-anchored.gif "mds_conc_recursive_UI_example_anchored")  
  
 Se você não ancorar relações nulas, os membros serão incluídos várias vezes. Todos os membros são exibidos no nível superior. Eles também são exibidos sob membros dos quais eles são atributos.  
  
 ![mds_conc_recursive_UI_example_nonanchored](../master-data-services/media/mds-conc-recursive-ui-example-nonanchored.gif "mds_conc_recursive_UI_example_nonanchored")  
  
 Neste exemplo, Marcia está no nível superior. Ela não é gerente de nenhum funcionário porque não é usada como um valor de atributo baseado em domínio para qualquer outro Funcionário membro. Por outro lado, Robert tem um nível abaixo dele porque Marcia tem Robert como seu valor de atributo de Gerente.  
  
## <a name="rules"></a>Regras  
  
-   Uma hierarquia derivada não pode conter mais de uma relação recursiva. Entretanto, ela pode ter outras relações derivadas (por exemplo, uma hierarquia derivada que contém uma relação recursiva Gerenciador para Funcionário também pode ter relações País para Gerenciador e Funcionário para Repositório).  
  
-   Você não pode atribuir permissões (na guia **Membros da Hierarquia** ) a membros de uma hierarquia recursiva.  
  
-   Hierarquias recursivas não podem incluir relações circulares. Por exemplo, Katherine não poderá ser o gerente de Sandeep se Sandeep for o gerente dela. Katherine também não pode ser gerente de si mesma.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Criar uma hierarquia derivada.|[Criar uma hierarquia derivada &#40;Master Data Services&#41;](../master-data-services/create-a-derived-hierarchy-master-data-services.md)|  
|Alterar o nome de uma hierarquia derivada existente.|[Alterar o nome de uma hierarquia derivada &#40;Master Data Services&#41;](../master-data-services/change-a-derived-hierarchy-name-master-data-services.md)|  
|Excluir uma hierarquia derivada existente.|[Excluir uma hierarquia derivada &#40;Master Data Services&#41;](../master-data-services/delete-a-derived-hierarchy-master-data-services.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Atributos baseados em domínio &#40;Master Data Services&#41;](../master-data-services/domain-based-attributes-master-data-services.md)  
  
-   [Hierarquias derivadas &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)  
  
  
