---
title: "Conceder acesso ao usuário a um servidor de relatório | Microsoft Docs"
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- removing role assignments
- permissions [Reporting Services], granting report server access
- roles [Reporting Services], assignments
- modifying role assignments
- deleting role assignments
ms.assetid: 2144c020-3253-4b47-8cda-e14c928bb471
caps.latest.revision: "54"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.openlocfilehash: a92c37165b8142b7e96a8bb99dee43ea5f12e247
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="grant-user-access-to-a-report-server"></a>Conceder acesso ao usuário a um servidor de relatório

[!INCLUDE[ssrs-appliesto-sql2016-preview](../../includes/ssrs-appliesto-sql2016-preview.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa a segurança baseada em função para conceder acesso de usuário a um servidor de relatório. Em uma nova instalação do servidor de relatório, somente os usuários que são membros do grupo Administradores local têm permissões no conteúdo e nas operações do servidor de relatório. Para disponibilizar o servidor de relatório a outros usuários, é necessário criar atribuições de função que mapeiem contas de usuário ou grupo para uma função predefinida que especifica uma coleção de tarefas.

 **Servidores de relatório do modo do SharePoint:** para um servidor de relatório configurado para o modo integrado do SharePoint, configure o acesso a partir de um site do SharePoint usando permissões do SharePoint. Os níveis de permissão no site do SharePoint determinam o acesso ao conteúdo e às operações de servidor de relatório. Você deve ser um administrador de site para conceder permissões em um site do SharePoint. Para obter mais informações, consulte [Concedendo permissões para itens do servidor de relatório em um site do SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md).

 **Servidores de relatório no modo nativo:** este tópico destina-se a um servidor de relatório configurado para o modo nativo e o uso do portal da Web para atribuir usuários a uma função. Existem dois tipos de funções:

- As funções do nível de item são usadas para exibir, adicionar e gerenciar o conteúdo do servidor de relatório, as assinaturas, o processamento de relatórios e o histórico de relatórios. As atribuições de função do nível de item são definidas no nó raiz (a pasta Base) ou em pastas ou itens específicos mais distantes da hierarquia.

- As funções do nível de sistema concedem acesso a operações do site inteiro que não são associadas a nenhum item específico. Os exemplos incluem o uso do Construtor de Relatórios e de agendas compartilhadas.

    Os dois tipos de função se complementam e devem ser usados juntos. Por este motivo, a adição de um usuário a um servidor de relatório é uma operação de duas partes. Se você atribuir um usuário a uma função do nível de item, também deve atribuí-lo a uma função do nível de sistema. Ao atribuir um usuário a uma função, selecione uma função que já está definida. Para criar, modificar ou excluir funções, use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Para obter mais informações, consulte [Criar, excluir ou modificar uma função &#40;Management Studio&#41;](../../reporting-services/security/role-definitions-create-delete-or-modify.md).

## <a name="before-you-start"></a>Antes de iniciar

Revise a lista a seguir antes de adicionar usuários a um servidor de relatório no modo nativo.

- Você deve ser um membro do grupo Administradores local no computador do servidor de relatório. Se estiver implantando o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] ou no Windows Server 2008, uma configuração adicional é necessária antes de administrar um servidor de relatório localmente. Para obter mais informações, consulte [Configurar um servidor de relatório no modo nativo para a Administração Local](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).

- Para delegar essa tarefa a outros usuários, crie atribuições de função que mapeiam contas de usuário para as funções Gerenciador de Conteúdo e Administrador do Sistema. Os usuários que têm as permissões Gerenciador de Conteúdo e Administrador do Sistema podem adicionar usuários a um servidor de relatório.

- No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], exiba as funções predefinidas para Funções do Sistema e Funções de Usuários para se familiarizar com os tipos de tarefas de cada função. As descrições de tarefa não são visíveis no portal da Web, de modo que é recomendado conhecer as funções antes de começar a adicionar usuários.

- Se preferir, personalize as funções ou defina funções adicionais para incluir a coleção de tarefas necessárias. Por exemplo, se você pretende usar configurações de segurança personalizadas para itens individuais, crie uma nova definição de função que conceda acesso de exibição às pastas.

### <a name="to-add-a-user-or-group-to-a-system-role"></a>Para adicionar um usuário ou grupo a uma função de sistema

1. Inicie o [portal da Web](../web-portal-ssrs-native-mode.md).

2. Selecione o *ícone de engrenagem* no canto superior direito.

3. Selecione **Configurações de Site**.

4. Selecione **Segurança**.

5. Selecione **Adicionar grupo ou usuário**.

6. Em **Grupo ou usuário**, insira uma conta de usuário ou grupo de domínio do Windows neste formato: \<domain>\\<account\>. 

    > [!NOTE]
    > Se estiver usando a autenticação de formulários ou a segurança personalizada, especifique a conta de usuário ou grupo no formato correto de sua implantação.

7. Selecione uma função de sistema e, em seguida, **OK**.

    As funções são cumulativas; desse modo, se você selecionar Administrador do Sistema e Usuário do Sistema, um usuário ou grupo poderá executar tarefas nas duas funções.

8. Repita o procedimento para criar atribuições para usuários ou grupos adicionais.

### <a name="to-add-a-user-or-group-to-an-item-role"></a>Para adicionar um usuário ou grupo a uma função de item

1. Inicie o **portal da Web** e localize o item de relatório ao qual você deseja adicionar um usuário ou grupo.

2. Selecione as **...** (reticências) em um item.

3. No menu suspenso, selecione **Gerenciar**.

4. Selecione **Segurança**.

5. Selecione **Adicionar grupo ou usuário**.

    > [!NOTE]
    > Se um item atualmente herdar a segurança de um item pai, selecione **Personalizar segurança** na barra de ferramentas para alterar as configurações de segurança. Em seguida, selecione **Adicionar grupo ou usuário**.

6. Em **Grupo ou usuário**, insira uma conta de usuário ou grupo de domínio do Windows neste formato: \<domain>\\<account\>. Se estiver usando a autenticação de formulários ou a segurança personalizada, especifique a conta de usuário ou grupo no formato correto de sua implantação.

7. Selecione uma ou mais definições de função que descrevem como o usuário ou grupo deve acessar o item e, em seguida, selecione **OK**.

8. Repita o procedimento para criar atribuições para usuários ou grupos adicionais.

## <a name="next-steps"></a>Próximas etapas

[Criar e gerenciar atribuições de função](../../reporting-services/security/create-and-manage-role-assignments.md)   
[Página Atribuição de Nova Função: Editar Atribuição de Função &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/3319ced0-4b86-42af-b18d-da41a625113c)   
[Página Propriedades de Segurança, Itens &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/351b8503-354f-4b1b-a7ac-f1245d978da0)   
[Atribuições de função](../../reporting-services/security/role-assignments.md)   
[Definições de função](../../reporting-services/security/role-definitions.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)