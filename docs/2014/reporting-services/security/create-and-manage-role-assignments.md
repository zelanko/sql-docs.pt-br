---
title: Criar e gerenciar atribuições de função | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- removing role assignments
- roles [Reporting Services], assignments
- security [Reporting Services], role assignments
- modifying role assignments
- deleting role assignments
ms.assetid: 086d0987-b43c-4834-8372-e08fb4b432f8
caps.latest.revision: 38
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 947216cb426750807e99b48ae2e691a5903ed3a5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37216506"
---
# <a name="create-and-manage-role-assignments"></a>Criar e gerenciar atribuições de função
  Uma *atribuição de função* é uma política de segurança que determina se um usuário ou grupo pode acessar um item de servidor de relatório específico ou executar uma operação. Uma atribuição de função consiste em um único nome de conta de usuário ou grupo e em uma ou mais definições de função.  
  
 As atribuições de função podem afetar o *nível do item* ou o *nível do sistema*.  
  
-   Uma atribuição de função em nível de item sempre é criada no contexto de um item ou ramificação específica na hierarquia de pastas do servidor de relatório. Navegue até uma pasta específica ou item para criar uma atribuição de função.  
  
-   As atribuições de função no nível do sistema fornecem aos usuários selecionados a possibilidade de executar tarefas que afetam o site de servidor de relatório como um todo. Essas tarefas incluem a criação de agendas compartilhadas, o gerenciamento de trabalhos, o processamento de relatórios no Construtor de Relatórios e a definição de propriedades. A segurança no nível do sistema não permite o acesso a itens na hierarquia de pastas do servidor de relatório.  
  
## <a name="creating-an-item-level-role-assignment"></a>Criando uma atribuição de função em nível de item  
 Para criar ou gerenciar atribuições de função, use o Gerenciador de Relatórios e abra as páginas de propriedade de Segurança do item que deseja proteger.  
  
 Você deve criar uma atribuição de função separada para cada conta de usuário ou grupo que requer acesso ao servidor de relatório. Se a conta estiver em um domínio diferente do domínio que contém o servidor de relatório, inclua o nome de domínio. Depois de especificar uma conta, você pode escolher uma ou mais definições de função. As definições de função são aditivas. O conjunto combinado de todas as tarefas de todas as definições é suportado na atribuição para um grupo ou usuário específico.  
  
 Para permitir o acesso completo, escolha um item que esteja no nível superior da hierarquia de pastas (por exemplo, o nó raiz Início). Você pode criar atribuições de função subsequentes para bloquear áreas específicas de nível inferior da hierarquia de pastas.  
  
 Você deve ser membro do grupo de Administradores local no computador do servidor de relatório para criar uma atribuição de função. Você pode delegar essa responsabilidade atribuindo outros usuários à função **Gerenciador de Conteúdo** .  
  
 Para obter mais informações, consulte [Grant User Access to a Report Server &#40;Report Manager&#41;](grant-user-access-to-a-report-server.md).  
  
## <a name="creating-a-system-level-role-assignment"></a>Criando uma atribuição de função no nível do sistema  
 Para criar ou gerenciar uma atribuição de função no nível do sistema, use o Gerenciador de Relatórios e abra a página Configurações de Site.  
  
 As atribuições de função em nível de sistema e de item são criadas juntas. Você deve criar uma atribuição de função em nível de sistema para cada usuário ou grupo que tem uma atribuição de função em nível de item.  
  
 As atribuições de função em nível de sistema incluem uma ampla variedade de permissões, mas não incluem permissões que fazem parte de uma atribuição de função em nível de item. Em contraste com as permissões de sistema em um computador, as funções de sistema no servidor de relatório não concedem permissões de longo alcance que incluem o conjunto completo de todas as operações possíveis. Em vez disso, as atribuições de função no nível do sistema simplesmente são um conjunto de tarefas que afetam o site do servidor de relatório. As permissões que são concedidas através de atribuições de função de sistema determinam se os usuários podem exibir propriedades de aplicativo (como a imagem ou o título da home page), exibir ou gerenciar agendas compartilhadas ou usar o Construtor de Relatórios.  
  
 Para obter mais informações, consulte [conceder acesso de usuário para um servidor de relatório &#40;Gerenciador de relatórios&#41; ](grant-user-access-to-a-report-server.md) e [funções predefinidas](role-definitions-predefined-roles.md).  
  
## <a name="modifying-a-role-assignment"></a>Modificando atribuições de função  
 Você pode modificar uma atribuição de função a qualquer momento. Suas alterações entram em vigor quando você salva a atribuição de função. As sessões de usuário não são afetadas pelas alterações da atribuição de função. Se um usuário tiver um relatório aberto e você modificar uma atribuição de função para negar o acesso, o usuário pode continuar usando o relatório contanto que a sessão esteja ativa.  
  
 Se você adicionar uma conta de usuário a um grupo que já faz parte de uma atribuição de função, haverá um retardo antes que a conta de usuário consiga acessar itens através das políticas da conta de grupo. Esse retardo é causado pelo armazenamento em cache do IIS de tokens de autenticação. Você pode aguardar a atualização dos tokens (normalmente, um período de 15 minutos) ou redefinir o IIS para atualizar o cache imediatamente.  
  
 Você pode modificar só uma atribuição de função de cada vez. Não é possível executar uma operação de localização e substituição global para alterar nomes de definição de função ou configurações de atribuição de função, nem para localizar todas as atribuições de função que incluem um usuário ou grupo específico.  
  
## <a name="deleting-a-role-assignment"></a>Excluindo atribuições de função  
 Você pode excluir atribuições de função marcando a caixa de seleção de cada atribuição que deseja excluir e clicando em **Excluir**. Você também pode excluir atribuições de função clicando em **Reverter em Segurança Pai**. Ao clicar nesse botão, as atribuições de função existentes para o item são excluídas e as atribuições fornecidas por um item pai são usadas.  
  
## <a name="see-also"></a>Consulte também  
 [Conceder acesso ao usuário a um servidor de relatório &#40;Gerenciador de Relatórios&#41;](grant-user-access-to-a-report-server.md)   
 [Modificar ou excluir uma atribuição de função &#40;Gerenciador de Relatórios&#41;](role-assignments-modify-or-delete.md)   
 [Atribuições de função](role-assignments.md)   
 [Definições de função](role-definitions.md)   
 [Funções predefinidas](role-definitions-predefined-roles.md)   
 [Conceder permissões em um servidor de relatório no Modo Nativo](granting-permissions-on-a-native-mode-report-server.md)  
  
  
