---
title: Atribuições de função | Microsoft Docs
ms.date: 05/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- users [Reporting Services]
- roles [Reporting Services]
- role-based security [Reporting Services], role assignments
- groups [Reporting Services]
- security [Reporting Services], role assignments
ms.assetid: 600e112c-1897-48a6-93c0-6e9f3f12dc01
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 810dd88b7572ea6af6ed5c5ac8a669a9c598b695
ms.sourcegitcommit: 603d5ef9b45c2f111d36d11864dc032917e4a321
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/08/2019
ms.locfileid: "65449670"
---
# <a name="role-assignments"></a>Atribuições de função

No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], as *atribuições de função* determinam o acesso aos itens armazenados e ao próprio servidor de relatório. Uma atribuição de função tem as seguintes partes:  
  
- Um item protegível para o qual você quer controlar o acesso. Exemplos de itens protegíveis: pastas, relatórios e recursos.  
  
- Um usuário ou conta de grupo que podem ser autenticados pela segurança do Windows ou outro mecanismo de autenticação.  
  
- As definições de função configuram um conjunto de tarefas permitidas e incluem:
  - **Navegador**
  - **Gerenciador de Conteúdo**
  - **Meus Relatórios**
  - **Publicador**
  - **Construtor de Relatórios**
  - **Administrador do Sistema**
  - **Usuário do Sistema**

 As atribuições de função são herdadas dentro da hierarquia de pasta de forma automática por conter:

- **Relatórios**
- **Fontes de dados compartilhadas**
- **Recursos**
- **Subpastas**

Você pode substituir a segurança herdada definindo atribuições de função para itens individuais. Todas as partes da hierarquia de pastas devem ser protegidas por pelo menos uma atribuição de função. Você não pode criar um item desprotegido ou manipular as configurações de uma forma que produza um item desprotegido.  
  
 O diagrama a seguir demonstra uma atribuição de função que mapeia um grupo e um usuário específico para a função **Publicador** para a Pasta B.  
  
 ![Diagrama de atribuições de função](../../reporting-services/security/media/report-securityarch.gif "Diagrama de atribuições de função")  
Diagrama de atribuições de função  
  
## <a name="system-level-and-item-level-role-assignments"></a>Atribuições de função de nível de sistema e de nível de item

 A segurança com base em função no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é organizada nos seguintes níveis:

- Atribuições de função de nível de item controlam o acesso aos itens na hierarquia de pasta do servidor de relatório, como:
  - relatórios
  - pastas
  - modelos de relatório
  - fontes de dados compartilhadas
  - outros recursos

- As atribuições de função do nível de item são definidas durante a criação de uma atribuição de função em um item específico ou na pasta Base.

- As atribuições de função de sistema autorizam as operações que estão no escopo do servidor como um todo. Por exemplo, a capacidade de gerenciar trabalhos é uma operação de nível de sistema. Uma atribuição de função de sistema não é o equivalente de um administrador de sistema. Ela não confere permissões avançadas que concedem controle total de um servidor de relatório.

Uma atribuição de função de sistema não autoriza o acesso aos itens na hierarquia de pastas. A segurança do sistema e do item é mutuamente exclusivas. Algumas vezes, pode ser necessário criar uma atribuição de função de nível de sistema e de item para fornecer acesso suficiente para um usuário ou grupo.

## <a name="users-and-groups-in-role-assignments"></a>Usuários e grupos em atribuições de função

 Os usuários ou contas de grupo que você especifica nas atribuições de função são contas de domínio. O servidor de relatório referencia, mas não cria nem gerencia, usuários e grupos de um domínio do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows (ou outro modelo de segurança caso você esteja usando uma extensão de segurança personalizada).

De todas as atribuições de função aplicáveis a um determinado item, não há duas que especifiquem o mesmo usuário ou grupo. Se uma conta de usuário também for membro de uma conta de grupo, e você tiver atribuições de função para ambas, o conjunto combinado de tarefas para essas duas atribuições estará disponível para o usuário.

Quando você adiciona um usuário ou grupo que já tem uma atribuição de função, é necessário redefinir o IIS (Serviços de Informações da Internet) para que a nova atribuição de função tenha efeito.

## <a name="predefined-role-assignments"></a>Atribuições de função predefinidas

 Por padrão, as atribuições de função predefinidas são implementadas de modo a permitir que os administradores locais gerenciem o servidor de relatório. Você pode adicionar mais atribuições de função para conceder acesso a outros usuários.

 Para obter mais informações sobre as atribuições de função predefinidas que fornecem segurança padrão, consulte [Funções predefinidas](../../reporting-services/security/role-definitions-predefined-roles.md).  

## <a name="see-also"></a>Consulte Também

 [Criar, excluir ou modificar uma função &#40;Management Studio&#41;](../../reporting-services/security/role-definitions-create-delete-or-modify.md)

 [Modificar ou excluir uma atribuição de função &#40; do portal da Web do SSRS &#41;](../../reporting-services/security/role-assignments-modify-or-delete.md)

 [Definir permissões para itens do Servidor de Relatório em um site do SharePoint &#40;Reporting Services no modo integrado do SharePoint&#41;](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)

 [Conceder permissões em um servidor de relatório no Modo Nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
