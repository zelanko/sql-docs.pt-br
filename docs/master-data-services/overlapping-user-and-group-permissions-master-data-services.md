---
title: "Sobrepondo permissões de usuário e grupo (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- users [Master Data Services], resolving permissions
- permissions [Master Data Services], user and group overlaps
- groups [Master Data Services], resolving permissions
ms.assetid: 31c3cf7d-17d4-4474-b6a7-ffcb9fc45b37
caps.latest.revision: 7
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 1dcefd134dccc0ae8a7039758dcd987e09b90813
ms.contentlocale: pt-br
ms.lasthandoff: 09/07/2017

---
# <a name="overlapping-user-and-group-permissions-master-data-services"></a>Sobrepondo permissões de usuário e grupo (Serviços de Dados Mestre)
  As permissões de um usuário são baseadas em:  
  
-   Permissões das associações a grupos.  
  
-   Permissões atribuídas explicitamente ao usuário.  
  
 Se um usuário for membro de vários grupos, e esses grupos tiverem acesso ao [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], as seguinte regras serão aplicadas:  
  
-   **Negar** substitui todas as outras permissões. Se a permissão do objeto for **Negar** em um grupo, a permissão efetiva será Negar.  
  
-   A permissão de acesso é uma união de todas as permissões efetivas em um grupo. Se a permissão do objeto for **Criar** em um grupo e **Atualizar** em outro grupo, a permissão efetiva será **Criar** e **Atualizar**.  
  
 Essas regras se aplicam às guias **Modelos** e **Membros da Hierarquia** . As permissões são resolvidas para cada guia e, em seguida, combinadas. Para obter mais informações, consulte [Como as permissões são determinadas &#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md).  
  
> [!NOTE]  
>  Você pode visualizar a resolução do usuário e do grupo sobrepondo permissões na interface do usuário. As guias **Modelos** e **Membros da Hierarquia** têm uma lista suspensa na qual é possível escolher **Efetivo** para exibir as permissões efetivas.  
  
## <a name="example-1"></a>Exemplo 1  
 ![mds_conc_user_group_ex_1](../master-data-services/media/mds-conc-user-group-ex-1.gif "mds_conc_user_group_ex_1")  
  
 O usuário pertence ao Grupo 1 e ao Grupo 2.  
  
 O usuário tem a permissão **Leitura** para a entidade Produto.  
  
 O Grupo 1 tem permissão **Atualizar** para a entidade Produto.  
  
 O Grupo 2 tem a permissão **Leitura** para a entidade Produto.  
  
 Resultado: a permissão efetiva do usuário é **Atualizar** para a entidade Produto.  
  
## <a name="example-2"></a>Exemplo 2  
 ![mds_conc_user_group_ex_2](../master-data-services/media/mds-conc-user-group-ex-2.gif "mds_conc_user_group_ex_2")  
  
 O usuário pertence ao Grupo 1 e ao Grupo 2.  
  
 O usuário tem a permissão **Leitura** para a entidade Produto.  
  
 O Grupo 1 tem permissão **Atualizar** para a entidade Produto.  
  
 O Grupo 2 tem permissão **Negar** para a entidade Produto.  
  
 Resultado: a permissão efetiva do usuário é **Negar** para a entidade Produto.  
  
## <a name="example-3"></a>Exemplo 3  
 ![mds_conc_user_group_ex_3](../master-data-services/media/mds-conc-user-group-ex-3.gif "mds_conc_user_group_ex_3")  
  
 O usuário pertence ao Grupo 1 e ao Grupo 2.  
  
 O usuário permissão **Atualizar** para um grupo de membros em um nó de hierarquia.  
  
 O Grupo 1 tem permissão **Leitura** para um grupo de membros em um nó de hierarquia.  
  
 O Grupo 2 tem permissão **Leitura** para um grupo de membros em um nó de hierarquia.  
  
 Resultado: a permissão efetiva do usuário é **Atualizar** para os membros.  
  
## <a name="see-also"></a>Consulte também  
 [Como as permissões são determinadas &#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md)   
 [Sobrepondo permissões de modelo e membro &#40;Master Data Services&#41;](../master-data-services/overlapping-model-and-member-permissions-master-data-services.md)  
  
  

