---
title: Administradores
description: 'Saiba mais sobre os tipos de administradores no Master Data Services: administradores de modelo, administradores de entidade e superusuário.'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- administrators [Master Data Services], about administrators
- administrators [Master Data Services]
- models [Master Data Services], administrators
ms.assetid: d330aa4e-6ade-4b09-b376-1b15d6c78f7d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 7e65024ac3673e6579e614ad64931ab772b599f3
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193643"
---
# <a name="administrators-master-data-services"></a>Administradores (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Este artigo descreve os tipos de administradores no [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]: administradores de modelo, administradores de entidade e superusuário.  
  
## <a name="model-administrators"></a>Administradores de modelo  
 No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , um administrador de modelo é um usuário que tem permissão de **administrador** atribuída ao objeto de modelo de nível superior na guia **objetos de modelo** . Quando um usuário tem permissão de administrador em um modelo específico, todas as outras permissões nos objetos filho do modelo (permissões de objeto de modelo e de membro) são superadas pela permissão de **administrador** de modelo e efetivamente ignoradas.  
  
-   Se o usuário tiver acesso à área funcional **Gerenciador** , ele poderá adicionar, excluir e atualizar todos os dados mestre nessa área.  
  
-   Se o usuário tiver acesso a outras áreas funcionais, o usuário poderá executar todas as tarefas administrativas disponíveis na área funcional.  
  
 Cada modelo pode ter vários administradores. Cada usuário pode ser um administrador de modelo para um, vários ou todos os modelos na implantação do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
 Um usuário ou pode ser configurado como um administrador de modelo no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ou programaticamente. Para obter mais informações, consulte [Criar um administrador de modelo &#40;Master Data Services&#41;](../master-data-services/create-a-model-administrator-master-data-services.md).  
  
## <a name="entity-administrators"></a>Administradores de entidade  
 No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , um administrador de entidade é um usuário que tem permissões de administrador atribuídas ao objeto de entidade na guia objetos de modelo. Quando um usuário tem permissões de administrador para uma entidade, todas as outras permissões nos objetos filho da entidade (permissões de objeto de modelo e de membro) são substituídas pelas permissões de administrador e são ignoradas.  
  
-   Se o usuário tiver acesso à área funcional **Gerenciador** , ele poderá adicionar, excluir e atualizar todos os dados mestre nessa área.  
  
-   Se as alterações de entidade exigirem aprovação do administrador, um administrador de entidade pode examinar e, em seguida, aprovar ou rejeitar conjuntos de alterações.  
  
 Cada entidade pode ter vários administradores. Cada usuário pode ser um administrador de entidade para uma, várias ou todas as entidades.  
  
 Um usuário pode ser configurado como um administrador de entidade no [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] ou de forma programática. Para obter mais informações, consulte [Criar um administrador de entidades &#40;Master Data Services&#41;](../master-data-services/create-an-entity-administrator-master-data-services.md).  
  
## <a name="master-data-services-super-user"></a>Superusuário do Master Data Services  
 No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], você pode atribuir permissões a um usuário à área funcional Superusuário. Um usuário com permissões à área funcional Superusuário efetivamente tem permissão de Administrador em todos os modelos e permissões para todas as outras áreas funcionais. Para obter informações sobre as permissões para as áreas funcionais, consulte [Permissões de área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
 O superusuário padrão é especificado para a **Conta de Administrador** quando você cria o banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] usando o [Assistente para Criar Banco de Dados &#40;Master Data Services Configuration Manager&#41;](../master-data-services/create-database-wizard-master-data-services-configuration-manager.md).  
  
 O superusuário pode fazer o seguinte:  
  
-   Acesse todas as áreas funcionais.  
  
-   Adicione, exclua e atualize todos os dados mestre de todos os modelos na área funcional **Gerenciador** .  
  
 Você pode atribuir permissões de Superusuário a vários usuários e/ou grupos de usuários.  
  
## <a name="comparing-administrator-types"></a>Comparando tipos de administrador  
  
|Tipo de administrador|Descrição|  
|------------------------|-----------------|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Superusuário|As permissões atribuídas no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] não têm nenhum efeito sobre o acesso do administrador.<br /><br /> Pode ser um superusuário com base em permissões de área funcional atribuídas explicitamente ou em permissões herdadas de um grupo.<br /><br /> Tem, automaticamente, todas as permissões para todos os modelos.<br /><br /> Tem acesso automaticamente a todas as áreas funcionais.|  
|Administrador de modelo|Pode ser um administrador de modelo com base nas permissões de administrador atribuídas explicitamente ou nas permissões herdadas de um grupo.<br /><br /> Tem acesso somente a áreas funcionais às quais esse acesso é concedido.<br /><br /> Tem automaticamente todas as permissões para todos os objetos e membros no modelo específico.|  
|Administrador de entidade|Pode ser um administrador de entidade com base nas permissões de administrador atribuídas explicitamente ou nas permissões herdadas de um grupo.<br /><br /> Tem acesso somente a áreas funcionais às quais esse acesso é concedido.<br /><br /> Tem automaticamente todas as permissões para todos os objetos e membros na entidade específica.<br /><br /> Poderá aprovar os conjuntos de alterações pendentes se as alterações de entidade exigirem aprovação.|  
  
## <a name="external-resources"></a>Recursos externos  
 Postagem do blog, [Aprimoramentos de Segurança](/archive/blogs/e7/improvements-to-autoplay), em msdn.com.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um administrador de modelo &#40;Master Data Services&#41;](../master-data-services/create-a-model-administrator-master-data-services.md)   
 [Criar um banco de dados Master Data Services](../master-data-services/install-windows/create-a-master-data-services-database.md)   
 [Notificações &#40;Master Data Services&#41;](../master-data-services/notifications-master-data-services.md)  
  
