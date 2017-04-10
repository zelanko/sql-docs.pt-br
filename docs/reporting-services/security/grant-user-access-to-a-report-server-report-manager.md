---
title: "Conceder acesso ao usu&#225;rio a um servidor de relat&#243;rio (Gerenciador de Relat&#243;rios) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "removendo atribuições de função"
  - "permissões [Reporting Services], concedendo acesso ao servidor de relatório"
  - "funções [Reporting Services], atribuições"
  - "modificando atribuições de função"
  - "excluindo atribuições de função"
ms.assetid: 2144c020-3253-4b47-8cda-e14c928bb471
caps.latest.revision: 54
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 54
---
# Conceder acesso ao usu&#225;rio a um servidor de relat&#243;rio (Gerenciador de Relat&#243;rios)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa a segurança baseada em função para conceder acesso de usuário a um servidor de relatório. Em uma nova instalação do servidor de relatório, somente os usuários que são membros do grupo Administradores local têm permissões no conteúdo e nas operações do servidor de relatório. Para disponibilizar o servidor de relatório a outros usuários, é necessário criar atribuições de função que mapeiem contas de usuário ou grupo para uma função predefinida que especifica uma coleção de tarefas.  
  
 **Servidores de relatório do modo do SharePoint:** para um servidor de relatório configurado para o modo integrado do SharePoint, configure o acesso a partir de um site do SharePoint usando permissões do SharePoint. Os níveis de permissão no site do SharePoint determinam o acesso ao conteúdo e às operações de servidor de relatório. Você deve ser um administrador de site para conceder permissões em um site do SharePoint. Para obter mais informações, consulte [Concedendo permissões para itens do servidor de relatório em um site do SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md).  
  
 **Servidores de relatório do modo nativo:** este tópico destina-se a um servidor de relatório configurado para o modo nativo e o uso do Gerenciador de Relatórios para atribuir usuários a uma função. Existem dois tipos de funções:  
  
-   As funções do nível de item são usadas para exibir, adicionar e gerenciar o conteúdo do servidor de relatório, as assinaturas, o processamento de relatórios e o histórico de relatórios. As atribuições de função do nível de item são definidas no nó raiz (a pasta Base) ou em pastas ou itens específicos mais distantes da hierarquia.  
  
-   As funções do nível de sistema concedem acesso a operações do site inteiro que não são associadas a nenhum item específico. Os exemplos incluem o uso do Construtor de Relatórios e de agendas compartilhadas.  
  
     Os dois tipos de função se complementam e devem ser usados juntos. Por este motivo, a adição de um usuário a um servidor de relatório é uma operação de duas partes. Se você atribuir um usuário a uma função do nível de item, também deve atribuí-lo a uma função do nível de sistema. Ao atribuir um usuário a uma função, selecione uma função que já está definida. Para criar, modificar ou excluir funções, use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Para obter mais informações, consulte [Criar, excluir ou modificar uma função &#40;Management Studio&#41;](../../reporting-services/security/create-delete-or-modify-a-role-management-studio.md).  
  
## Antes de iniciar  
 Revise a lista a seguir antes de adicionar usuários a um servidor de relatório no modo nativo.  
  
-   Você deve ser um membro do grupo Administradores local no computador do servidor de relatório. Se estiver implantando o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] ou no Windows Server 2008, uma configuração adicional é necessária antes de administrar um servidor de relatório localmente. Para obter mais informações, veja [Configurar um servidor de relatório no modo nativo para a Administração Local &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
-   Para delegar essa tarefa a outros usuários, crie atribuições de função que mapeiam contas de usuário para as funções Gerenciador de Conteúdo e Administrador do Sistema. Os usuários que têm as permissões Gerenciador de Conteúdo e Administrador do Sistema podem adicionar usuários a um servidor de relatório.  
  
-   No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], exiba as funções predefinidas para Funções do Sistema e Funções de Usuários para se familiarizar com os tipos de tarefas de cada função. As descrições de tarefa não são visíveis no Gerenciador de Relatórios, de modo que é recomendado conhecer as funções antes de começar a adicionar usuários.  
  
-   Se preferir, personalize as funções ou defina funções adicionais para incluir a coleção de tarefas necessárias. Por exemplo, se você pretende usar configurações de segurança personalizadas para itens individuais, crie uma nova definição de função que conceda acesso de exibição às pastas.  
  
### Para adicionar um usuário ou grupo a uma função de sistema  
  
1.  Inicie o [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md).  
  
2.  Clique em **Configurações de Site**.  
  
3.  Clique em **Segurança**.  
  
4.  Clique em **Atribuição de Nova Função**.  
  
5.  Em **Nome de grupo ou de usuário**, insira uma conta de usuário ou grupo de domínio do Windows neste formato: \<domain>\\<account\>. Se estiver usando a autenticação de formulários ou a segurança personalizada, especifique a conta de usuário ou grupo no formato correto de sua implantação.  
  
6.  Selecione uma função de sistema e clique em **OK**.  
  
     As funções são cumulativas; desse modo, se você selecionar Administrador do Sistema e Usuário do Sistema, um usuário ou grupo poderá executar tarefas nas duas funções.  
  
7.  Repita o procedimento para criar atribuições para usuários ou grupos adicionais.  
  
### Para adicionar um usuário ou grupo a uma função de item  
  
1.  Inicie o **Gerenciador de Relatórios** e localize o item de relatório ao qual você deseja adicionar um usuário ou grupo.  
  
2.  Focalize o item e clique na seta do menu suspenso.  
  
3.  No menu suspenso, clique em **Segurança**.  
  
4.  Clique em **Atribuição de Nova Função**.  
  
    > [!NOTE]  
    >  Se um item atualmente herda a segurança de um item pai, clique em **Editar Segurança de Item** na barra de ferramentas para alterar as configurações de segurança. Em seguida, clique em **Atribuição de Nova Função**.  
  
5.  Em **Nome de grupo ou de usuário**, insira uma conta de usuário ou grupo de domínio do Windows neste formato: \<domain>\\<account\>. Se estiver usando a autenticação de formulários ou a segurança personalizada, especifique a conta de usuário ou grupo no formato correto de sua implantação.  
  
6.  Selecione uma ou mais definições de função que descrevam como o usuário ou grupo deve acessar o item e, em seguida, clique em **OK**.  
  
7.  Repita o procedimento para criar atribuições para usuários ou grupos adicionais.  
  
## Consulte também  
 [Criar e gerenciar atribuições de função](../../reporting-services/security/create-and-manage-role-assignments.md)   
 [Página Atribuição de Nova Função: Editar Atribuição de Função &#40;Gerenciador de Relatórios&#41;](../Topic/New%20Role%20Assignment:%20Edit%20Role%20Assignment%20Page%20\(Report%20Manager\).md)   
 [Página Propriedades de Segurança, Itens &#40;Gerenciador de Relatórios&#41;](../Topic/Security%20Properties%20Page,%20Items%20\(Report%20Manager\).md)   
 [Atribuições de função](../../reporting-services/security/role-assignments.md)   
 [Definições de função](../../reporting-services/security/role-definitions.md)  
  
  