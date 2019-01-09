---
title: Configurar regras de negócio para enviar notificações (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], configuring notifications
- e-mail [Master Data Services], configuring business rules
- notifications [Master Data Services], configuring business rules
ms.assetid: b24f7b11-ab53-4642-999c-e17b543b3558
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 25de38d04af8b98b600422a843c6b6fb6260d514
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52783458"
---
# <a name="configure-business-rules-to-send-notifications-master-data-services"></a>Configurar regras de negócio para enviar notificações (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], configure regras de negócios para enviar notificações quando você desejar notificar os usuários sobre alterações de valor de atributo.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar as áreas funcionais **Administração do Sistema** e **Permissões de Usuário e de Grupo** . Se você não tiver permissão para a área funcional **Permissões de Usuário e de Grupo** , não poderá exibir a lista de usuários e grupos para a qual enviar notificações.  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Uma regra de negócios que usa uma ação de validação já deve existir. Para obter mais informações, consulte [Criar e publicar uma regra de negócio &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md).  
  
-   O usuário ou grupo que recebe a notificação deve ter, no mínimo, a permissão **Somente leitura** no atributo que falhar na validação. Os usuários ou grupos que tiverem a permissão para o atributo negada de forma explícita ou implícita receberão o email, mas não poderão acessar o atributo no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
-   Se o email for enviado a um grupo, somente os membros do grupo que tiverem acessado o [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] receberão o email.  
  
### <a name="to-configure-business-rules-to-send-notifications"></a>Para configurar regras de negócios para enviar notificações  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na barra de menus, aponte para **Gerenciar** e clique em **Regras de Negócios**.  
  
3.  Na página **Regras de Negócio** , na lista **Modelo** , selecione um modelo.  
  
4.  Na lista suspensa **Entidade** , escolha uma entidade.  
  
5.  Na lista suspensa **Tipos de Membro** , escolha um tipo de membro.  
  
6.  Na grade, selecione a linha da regra de negócio que deseja editar e clique em **Editar**.  
  
7.  Marque a caixa de seleção **Enviar Notificações** e, na lista suspensa, selecione um usuário ou grupo ao qual a notificação por email será enviada.  
  
8.  Clique em **Salvar**.  
  
9. Clique em **Publicar Tudo**.  
  
10. Na caixa de diálogo de confirmação, clique em **OK**. O valor na coluna **Estado da Regra de Negócios** mudou para **Ativo** e a coluna **Notificação** mostra o usuário ou grupo selecionado ao qual enviar a notificação.  
  
## <a name="next-steps"></a>Next Steps  
  
-   Aplique regras de negócio a dados seguindo um destes procedimentos:  
  
    -   [Validar membros específicos em relação a regras de negócio &#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [Validar uma versão em relação a regras de negócio &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
-   Configure o protocolo de email da seguinte maneira:  
  
    -   [Configurar notificações por email &#40;Master Data Services&#41;](../master-data-services/configure-email-notifications-master-data-services.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Notificações &#40;Master Data Services&#41;](../master-data-services/notifications-master-data-services.md)   
 [Configurar notificações por email &#40;Master Data Services&#41;](../master-data-services/configure-email-notifications-master-data-services.md)  
  
  
