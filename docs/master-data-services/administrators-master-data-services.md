---
title: Administradores (Master Data Services) | Microsoft Docs
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
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 85ad4589ef25042498b132475af39cb36fd1b2bc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62817940"
---
# <a name="administrators-master-data-services"></a>Administradores (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Este artigo descreve os tipos de administradores no [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]: administradores de modelo, administradores de entidade e superusuário.  
  
## <a name="model-administrators"></a>Administradores de modelo  
 No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], um administrador de modelo é um usuário que tem a permissão **Administrador** atribuída ao objeto de modelo de nível superior na guia **Objetos de Modelo** . Quando um usuário tem permissão de administrador em um modelo específico, todas as outras permissões nos objetos filho do modelo (tanto permissões de objeto modelo quanto de membro) são superadas pela permissão **Administrador** do modelo e efetivamente ignoradas.  
  
-   Se o usuário tiver acesso à área funcional **Gerenciador** , ele poderá adicionar, excluir e atualizar todos os dados mestre nessa área.  
  
-   Se o usuário tiver acesso a outras áreas funcionais, o usuário poderá executar todas as tarefas administrativas disponíveis na área funcional.  
  
 Cada modelo pode ter vários administradores. Cada usuário pode ser um administrador de modelo para um, vários ou todos os modelos na implantação do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
 Um usuário ou pode ser configurado como um administrador de modelo no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ou programaticamente. Para obter mais informações, consulte [Criar um administrador de modelo &#40;Master Data Services&#41;](../master-data-services/create-a-model-administrator-master-data-services.md).  
  
## <a name="entity-administrators"></a>Administradores de entidade  
 No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], um administrador de entidade é um usuário que tem permissões de administrador atribuídas ao objeto de entidade na guia Objetos de Modelo. Quando um usuário tem permissões de administrador para uma entidade, quaisquer outras permissões nos objetos filho da entidade (tanto permissões de membro quanto de objeto modelo) são substituídas pelas permissões de administrador e são ignoradas.  
  
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
 Postagem do blog, [Aprimoramentos de Segurança](https://go.microsoft.com/fwlink/p/?LinkId=615376), em msdn.com.  
  
## <a name="see-also"></a>Consulte também  
 [Criar um administrador de modelo &#40;Master Data Services&#41;](../master-data-services/create-a-model-administrator-master-data-services.md)   
 [Criar um banco de dados do Master Data Services](../master-data-services/install-windows/create-a-master-data-services-database.md)   
 [Notificações &#40;Master Data Services&#41;](../master-data-services/notifications-master-data-services.md)  
  
  
