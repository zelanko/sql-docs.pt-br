---
title: Atribuições de função | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- users [Reporting Services]
- roles [Reporting Services]
- role-based security [Reporting Services], role assignments
- groups [Reporting Services]
- security [Reporting Services], role assignments
ms.assetid: 600e112c-1897-48a6-93c0-6e9f3f12dc01
caps.latest.revision: 36
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: d20737ae25412caa7af4c3aa82966a5b384d7126
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130907"
---
# <a name="role-assignments"></a>Atribuições de função
  No [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], as *atribuições de função* determinam o acesso aos itens armazenados e ao próprio servidor de relatório. Uma atribuição de função tem as seguintes partes:  
  
-   Um item protegível para o qual você quer controlar o acesso. Exemplos de itens protegíveis: pastas, relatórios e recursos.  
  
-   Um usuário ou conta de grupo que podem ser autenticados pela segurança do Windows ou outro mecanismo de autenticação.  
  
-   Definições de função que estabelecem um conjunto de tarefas. Exemplos de definições de função: **Administrador de Sistema**, **Gerente de Conteúdo**e **Publicador**.  
  
 As atribuições de função são herdadas dentro da hierarquia de pastas. A atribuição de função definida para uma pasta é herdada automaticamente por todos os relatórios, fontes de dados compartilhadas, recursos e subpastas contidos nessa pasta. Você pode substituir a segurança herdada definindo atribuições de função para itens individuais. Todas as partes da hierarquia de pastas devem ser protegidas por pelo menos uma atribuição de função. Você não pode criar um item desprotegido ou manipular as configurações de uma forma que produza um item desprotegido.  
  
 O diagrama a seguir demonstra uma atribuição de função que mapeia um grupo e um usuário específico para a função **Publicador** para a Pasta B.  
  
 ![Diagrama de atribuições de função](../media/report-securityarch.gif "Diagrama de atribuições de função")  
Diagrama de atribuições de função  
  
## <a name="system-level-and-item-level-role-assignments"></a>Atribuições de função de nível de sistema e de nível de item  
 A segurança com base em função no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] é organizada nos seguintes níveis:  
  
-   As atribuições de função de nível de item controlam o acesso aos relatórios, pastas, modelos de relatório, fontes de dados compartilhadas e recursos na hierarquia de pastas do servidor de relatório. As atribuições de função do nível de item são definidas durante a criação de uma atribuição de função em um item específico ou na pasta Base.  
  
-   As atribuições de função de sistema autorizam as operações que têm escopo no servidor como um todo (por exemplo, a capacidade de gerenciar trabalhos é uma operação de nível de sistema). Uma atribuição de função de sistema não é o equivalente de um administrador de sistema. Ela não confere permissões avançadas que concedem controle total de um servidor de relatório.  
  
 Uma atribuição de função de sistema não autoriza o acesso aos itens na hierarquia de pastas. A segurança do sistema e do item é mutuamente exclusivas. Para qualquer usuário ou grupo determinado, talvez seja necessário criar uma atribuição de função de nível de sistema e de item para fornecer acesso suficiente para um servidor de relatório.  
  
## <a name="users-and-groups-in-role-assignments"></a>Usuários e grupos em atribuições de função  
 Os usuários ou contas de grupo que você especifica nas atribuições de função são contas de domínio. O servidor de relatório referencia, mas não cria nem gerencia, usuários e grupos de um domínio do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows (ou outro modelo de segurança caso você esteja usando uma extensão de segurança personalizada).  
  
 De todas as atribuições de função aplicáveis a um determinado item, não há duas que especifiquem o mesmo usuário ou grupo. Se uma conta de usuário também for membro de uma conta de grupo, e você tiver atribuições de função para ambas, o conjunto combinado de tarefas para essas duas atribuições estará disponível para o usuário.  
  
 Quando você adiciona um usuário ou grupo que já faça parte de uma atribuição de função, é necessário redefinir o IIS (Serviços de Informações da Internet) para que a nova atribuição de função tenha efeito para esse usuário.  
  
## <a name="predefined-role-assignments"></a>Atribuições de função predefinidas  
 Por padrão, as atribuições de função predefinidas são implementadas de modo a permitir que os administradores locais gerenciem o servidor de relatório. Você deve adicionar mais atribuições de função para conceder acesso a outros usuários.  
  
 Para obter mais informações sobre as atribuições de função predefinida que fornecem segurança padrão, consulte [funções predefinidas](role-definitions-predefined-roles.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criar, excluir ou modificar uma função &#40;Management Studio&#41;](role-definitions-create-delete-or-modify.md)   
 [Conceder acesso ao usuário a um servidor de relatório &#40;Gerenciador de Relatórios&#41;](grant-user-access-to-a-report-server.md)   
 [Modificar ou excluir uma atribuição de função &#40;Gerenciador de Relatórios&#41;](role-assignments-modify-or-delete.md)   
 [Definir permissões para itens do servidor de relatório em um Site do SharePoint &#40;Reporting Services no SharePoint modo integrado&#41;](set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
 [Conceder permissões em um servidor de relatório no Modo Nativo](granting-permissions-on-a-native-mode-report-server.md)  
  
  