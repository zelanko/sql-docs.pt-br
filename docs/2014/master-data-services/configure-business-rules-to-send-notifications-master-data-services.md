---
title: Configurar regras de negócio para enviar notificações (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], configuring notifications
- e-mail [Master Data Services], configuring business rules
- notifications [Master Data Services], configuring business rules
ms.assetid: b24f7b11-ab53-4642-999c-e17b543b3558
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: b0ea6e215b5192d1b9e84ed252708b188d5c5a59
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65483950"
---
# <a name="configure-business-rules-to-send-notifications-master-data-services"></a>Configurar regras de negócio para enviar notificações (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], configure regras de negócios para enviar notificações quando você desejar notificar os usuários sobre alterações de valor de atributo.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar as áreas funcionais **Administração do Sistema** e **Permissões de Usuário e de Grupo** . Se você não tiver permissão para a área funcional **Permissões de Usuário e de Grupo** , não poderá exibir a lista de usuários e grupos para a qual enviar notificações.  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   Uma regra de negócios que usa uma ação de validação já deve existir. Para obter mais informações, consulte [Criar e publicar uma regra de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md).  
  
-   O usuário ou grupo que recebe a notificação deve ter, no mínimo, a permissão **Somente leitura** no atributo que falhar na validação. Os usuários ou grupos que tiverem a permissão para o atributo negada de forma explícita ou implícita receberão o email, mas não poderão acessar o atributo no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
-   Se o email for enviado a um grupo, somente os membros do grupo que tiverem acessado o [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] receberão o email.  
  
### <a name="to-configure-business-rules-to-send-notifications"></a>Para configurar regras de negócios para enviar notificações  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na barra de menus, aponte para **Gerenciar** e clique em **Regras de Negócios**.  
  
3.  Na página **Manutenção de Regra de Negócio** , na lista **Modelo** , selecione um modelo.  
  
4.  Na lista **Entidade** , selecione uma entidade.  
  
5.  Dos **tipo de membro** , selecione um tipo de membro.  
  
6.  Na lista **Atributo** , selecione um atributo ou deixe o valor padrão **Todos**.  
  
7.  Na grade, na linha da regra de negócio, clique duas vezes o **notificação** campo.  
  
8.  No submenu, clique em um usuário ou grupo para o qual enviar a notificação por email.  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   Aplique regras de negócio a dados seguindo um destes procedimentos:  
  
    -   [Validar membros específicos em relação a regras de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [Validar uma versão em relação a regras de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
-   Configure o protocolo de email da seguinte maneira:  
  
    -   [Configurar notificações por email &#40;Master Data Services&#41;](../../2014/master-data-services/configure-email-notifications-master-data-services.md)  
  
## <a name="see-also"></a>Consulte também  
 [Notificações &#40;Master Data Services&#41;](../../2014/master-data-services/notifications-master-data-services.md)   
 [Configurar notificações por email &#40;Master Data Services&#41;](../../2014/master-data-services/configure-email-notifications-master-data-services.md)  
  
  
