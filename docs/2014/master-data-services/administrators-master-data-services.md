---
title: Administradores (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- administrators [Master Data Services], about administrators
- administrators [Master Data Services]
- models [Master Data Services], administrators
ms.assetid: d330aa4e-6ade-4b09-b376-1b15d6c78f7d
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 676af20a08829dcc1bd4fda019c4f42b5d51eb51
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48083517"
---
# <a name="administrators-master-data-services"></a>Administradores (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], há dois tipos de administradores: administradores de modelo e o administrador do sistema do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
## <a name="model-administrators"></a>Administradores de modelo  
 Na [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], um administrador de modelo é um usuário que tem **Update** permissão atribuída ao objeto de modelo de nível superior no **objetos de modelo** guia e nenhuma outra receber permissões.  
  
-   Se o usuário tiver acesso à área funcional **Gerenciador** , ele poderá adicionar, excluir e atualizar todos os dados mestre nessa área.  
  
-   Se o usuário tiver acesso a outras áreas funcionais, o usuário poderá executar todas as tarefas administrativas disponíveis na área funcional.  
  
 Cada modelo pode ter vários administradores. Cada usuário pode ser um administrador de modelo para um, vários ou todos os modelos na implantação do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
 Um usuário ou pode ser configurado como um administrador de modelo no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ou programaticamente. Para obter mais informações, consulte [Create a Model Administrator &#40;Master Data Services&#41;](create-a-model-administrator-master-data-services.md).  
  
## <a name="master-data-services-system-administrator"></a>Administrador do sistema do Master Data Services  
 Há somente um administrador do sistema [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. O administrador do sistema é o usuário especificado para o **conta de administrador** quando você cria o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] banco de dados.  
  
 O administrador do sistema do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]:  
  
-   Tem acesso automaticamente a todas as áreas funcionais.  
  
-   Pode adicionar, excluir e atualizar todos os dados mestres para todos os modelos na **Explorer** área funcional.  
  
 Você pode alterar o usuário designado como administrador do sistema. Para obter mais informações, consulte [alterar a conta de administrador do sistema &#40;Master Data Services&#41;](../../2014/master-data-services/change-the-system-administrator-account-master-data-services.md).  
  
## <a name="comparing-administrator-types"></a>Comparando tipos de administrador  
  
|Tipo de administrador|Description|  
|------------------------|-----------------|  
|Administrador do sistema [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|As permissões atribuídas no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] não têm nenhum efeito sobre o acesso do administrador.<br /><br /> Tem automaticamente **atualização** permissão a todos os modelos.<br /><br /> Tem acesso automaticamente a todas as áreas funcionais.<br /><br /> Em tbluser, o valor de **ID** coluna é **1**.|  
|Administrador de modelo|As permissões atribuídas no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] determinam se o usuário é um administrador de modelo.<br /><br /> Pode ser um administrador de modelo com base nas permissões atribuídas explicitamente ou nas permissões herdadas de um grupo.<br /><br /> É um administrador somente para modelos que têm **atualização** permissão atribuída ao objeto de modelo de nível superior e nenhuma outra permissão.<br /><br /> Tem acesso somente a áreas funcionais às quais esse acesso é concedido.<br /><br /> Em tbluser, o valor de **ID** coluna não é **1**.|  
  
## <a name="see-also"></a>Consulte também  
 [Criar um administrador de modelo &#40;Master Data Services&#41;](create-a-model-administrator-master-data-services.md)   
 [Alterar a conta de administrador do sistema &#40;Master Data Services&#41;](../../2014/master-data-services/change-the-system-administrator-account-master-data-services.md)   
 [Criar um banco de dados do Master Data Services](install-windows/create-a-master-data-services-database.md)   
 [Notificações &#40;Master Data Services&#41;](../../2014/master-data-services/notifications-master-data-services.md)  
  
  
