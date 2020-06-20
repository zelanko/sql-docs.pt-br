---
title: Administradores (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: aeedc1f735fd296169f704b794d1bb0e69adab22
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972266"
---
# <a name="administrators-master-data-services"></a>Administradores (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], há dois tipos de administradores: administradores de modelo e o administrador do sistema do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
## <a name="model-administrators"></a>Administradores de modelo  
 No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , um administrador de modelo é um usuário que tem a permissão **Atualizar** atribuída ao objeto de modelo de nível superior na guia **objetos de modelo** e nenhuma outra permissão atribuída.  
  
-   Se o usuário tiver acesso à área funcional **Gerenciador** , ele poderá adicionar, excluir e atualizar todos os dados mestre nessa área.  
  
-   Se o usuário tiver acesso a outras áreas funcionais, o usuário poderá executar todas as tarefas administrativas disponíveis na área funcional.  
  
 Cada modelo pode ter vários administradores. Cada usuário pode ser um administrador de modelo para um, vários ou todos os modelos na implantação do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
 Um usuário ou pode ser configurado como um administrador de modelo no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ou programaticamente. Para obter mais informações, consulte [Criar um administrador de modelo &#40;Master Data Services&#41;](create-a-model-administrator-master-data-services.md).  
  
## <a name="master-data-services-system-administrator"></a>Administrador do sistema do Master Data Services  
 Há somente um administrador do sistema [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. O administrador do sistema é o usuário especificado para a **conta de administrador** quando você cria o banco de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] dados.  
  
 O administrador do sistema do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]:  
  
-   Tem acesso automaticamente a todas as áreas funcionais.  
  
-   Pode adicionar, excluir e atualizar todos os dados mestre de todos os modelos na área funcional do **Gerenciador** .  
  
 Você pode alterar o usuário designado como administrador do sistema. Para obter mais informações, consulte [alterar a conta de administrador do sistema &#40;Master Data Services&#41;](../../2014/master-data-services/change-the-system-administrator-account-master-data-services.md).  
  
## <a name="comparing-administrator-types"></a>Comparando tipos de administrador  
  
|Tipo de administrador|Descrição|  
|------------------------|-----------------|  
|Administrador do sistema [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|As permissões atribuídas no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] não têm nenhum efeito sobre o acesso do administrador.<br /><br /> Tem automaticamente a permissão **Atualizar** para todos os modelos.<br /><br /> Tem acesso automaticamente a todas as áreas funcionais.<br /><br /> No MDM. tblUser, o valor na coluna **ID** é **1**.|  
|Administrador de modelo|As permissões atribuídas no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] determinam se o usuário é um administrador de modelo.<br /><br /> Pode ser um administrador de modelo com base nas permissões atribuídas explicitamente ou nas permissões herdadas de um grupo.<br /><br /> É um administrador somente para modelos que têm permissão de **atualização** atribuída ao objeto de modelo de nível superior e nenhuma outra permissão.<br /><br /> Tem acesso somente a áreas funcionais às quais esse acesso é concedido.<br /><br /> No MDM. tblUser, o valor na coluna **ID** não é **1**.|  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um administrador de modelo &#40;Master Data Services&#41;](create-a-model-administrator-master-data-services.md)   
 [Altere a conta de administrador do sistema &#40;Master Data Services&#41;](../../2014/master-data-services/change-the-system-administrator-account-master-data-services.md)   
 [Criar um banco de dados Master Data Services](install-windows/create-a-master-data-services-database.md)   
 [Notificações &#40;Master Data Services&#41;](../../2014/master-data-services/notifications-master-data-services.md)  
  
  
