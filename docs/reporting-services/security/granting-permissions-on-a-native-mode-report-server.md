---
description: Conceder permissões em um servidor de relatório no modo nativo
title: Conceder permissões em um servidor de relatório no modo nativo | Microsoft Docs
ms.date: 05/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- roles [Reporting Services], creating
- authorization [Reporting Services]
- server security [Reporting Services]
- role-based security [Reporting Services]
- items [Reporting Services], security
- permissions [Reporting Services], native mode
- published reports [Reporting Services], security
- reports [Reporting Services], security
- report items [Reporting Services], security
- role-based security [Reporting Services], about role-based security
- security [Reporting Services], role-based
ms.assetid: 260dc2e9-546c-4f04-9fa1-977e23c9d68c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 82fba1144cdb970d97b8aac4938fd7c3e8fe0980
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88373292"
---
# <a name="grant-permissions-on-a-native-mode-report-server"></a>Conceder permissões em um servidor de relatório no modo nativo
  O SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa autorização com base em funções e um subsistema de autenticação para determinar quem pode executar operações e acessar itens em um servidor de relatório. A autorização com base em funções é categorizada nas funções do conjunto de ações que um usuário ou grupo pode executar. A autenticação se baseia na Autenticação interna do Windows ou em um módulo de autenticação personalizado fornecido por você. É possível utilizar funções predefinidas ou personalizadas com qualquer tipo de autenticação.
  
## <a name="use-roles-to-grant-report-server-access"></a>Usar funções para conceder acesso ao servidor de relatório
 Todos os usuários interagem com um servidor de relatório dentro do contexto de uma função que define um nível específico de acesso. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclui funções predefinidas que podem ser atribuídas a usuários e grupos para fornecer acesso imediato a um servidor de relatório. **Gerenciador de Conteúdo**, **Editor** e **Navegador** são exemplos de funções predefinidas. Cada função define uma coleção de tarefas relacionadas. Por exemplo, um **Publicador** tem permissão para adicionar relatórios e criar pastas para armazenar esses relatórios.
  
 Em geral, as atribuições de funções são herdadas de um nó pai, mas você pode dividir a herança de permissões criando uma nova atribuição de função para um determinado item. Um usuário que é membro da função **Gerenciador de Conteúdo** de um relatório pode ser membro da função **Navegador** de outro relatório.
  
 Para permitir acesso a itens e operações de servidor de relatório:
  
1. Examine as funções predefinidas para determinar se você pode usá-las no estado em que se encontram. Se for necessário ajustar as tarefas ou definir funções adicionais, execute essas ações antes de começar a atribuir usuários a funções específicas. Para obter mais informações sobre cada função, confira [Funções predefinidas](../../reporting-services/security/role-definitions-predefined-roles.md).
  
1. Identifique quais usuários e grupos requerem acesso ao servidor de relatório, e em que nível. Atribua a maioria dos usuários à função **Navegador** ou à função **Construtor de Relatórios**. Atribua um número menor de usuários à função **Editor**. Atribua apenas alguns usuários à função do **Gerenciador de Conteúdo**.
  
1. Use o portal da Web para atribuir funções na pasta base para cada usuário ou grupo que exigir acesso. A pasta base é a pasta de nível superior da hierarquia de pastas do servidor de relatório.
  
1. No nível do site, na página **Configurações de Site** no portal da Web, crie uma atribuição de função no nível do sistema para cada usuário e grupo, usando as funções predefinidas **Usuário do Sistema** e **Administrador do Sistema**.
  
1. Crie atribuições de funções adicionais conforme o necessário para pastas, relatórios e outros itens específicos. Evite criar um número grande de atribuições de funções. Se você criar atribuições demais, será difícil controlar os diferentes níveis de permissão de cada usuário.
  
> [!NOTE]  
>  Se você tiver configurado um servidor de relatório para ser executado no modo integrado do SharePoint, defina permissões no site do SharePoint para conceder acesso aos itens de servidor de relatório. Para obter mais informações, confira [Conceder permissões para itens do servidor de relatório em um site do SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md).
> 
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.
  
## <a name="who-sets-permissions"></a>Quem define as permissões
 Inicialmente, apenas usuários que são os membros do grupo de administradores local podem acessar um servidor de relatório. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é instalado com duas atribuições de função padrão que concedem acesso em nível de item e do sistema a membros do grupo de administradores local. Os administradores locais podem usar essas atribuições de funções internas para conceder acesso ao servidor de relatório para outros usuários e gerenciar itens do servidor de relatório. Não é possível excluir as atribuições de funções internas. Um administrador local sempre tem permissão para gerenciar totalmente uma instância do servidor de relatório.
 
 A configuração adicional é necessária para que você possa administrar uma instância do servidor de relatório em um computador local com o Windows Vista ou o Windows Server 2008. Para obter mais informações, confira [Configurar um servidor de relatório no modo nativo para a administração local &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).
  
## <a name="how-permissions-are-stored"></a>Como as permissões são armazenadas
 As atribuições de funções e definições são armazenadas no banco de dados do servidor de relatório. Se você estiver usando várias ferramentas de clientes ou interfaces programáticas, todo o acesso estará sujeito às permissões definidas para a instância do servidor de relatório como um todo. Se você estiver configurando vários servidores de relatório em uma implantação de expansão, as atribuições de função definidas em uma instância serão armazenadas em um banco de dados compartilhado e usadas por todas as outras instâncias na mesma implantação de expansão. Como as atribuições de funções são armazenadas com os itens que protegem, você pode mover o banco de dados para outra instância do servidor de relatório sem perder as permissões definidas.
  
## <a name="tasks-and-tools-for-managing-permissions"></a>Tarefas e ferramentas para o gerenciamento de permissões
 Use as ferramentas a seguir para gerenciar definições e atribuições de funções.
  
|Ferramenta|Tarefas|  
|----------|-----------|  
|Management Studio: usado para exibir, modificar, criar e excluir definições de funções|[Criar, excluir ou modificar uma função &#40;Management Studio&#41;](../../reporting-services/security/role-definitions-create-delete-or-modify.md)|  
|O portal da Web: usado para atribuir usuários e grupos a funções|[Conceder acesso ao usuário a um servidor de relatório](../../reporting-services/security/grant-user-access-to-a-report-server.md)<br /><br /> [Modificar ou excluir uma atribuição de função](../../reporting-services/security/role-assignments-modify-or-delete.md)|  
  
## <a name="see-also"></a>Confira também
 - [Funções predefinidas](../../reporting-services/security/role-definitions-predefined-roles.md)  
 - [Conceder permissões para itens do servidor de relatório em um site do SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
 - [Autenticação com o servidor de relatório](../../reporting-services/security/authentication-with-the-report-server.md)  
 - [Criar e gerenciar atribuições de função](../../reporting-services/security/create-and-manage-role-assignments.md)  
 - [Segurança e proteção do Reporting Services](../../reporting-services/security/reporting-services-security-and-protection.md)  
 - [Gerenciamento de conteúdo do Servidor de Relatório &#40;modo nativo do SSRS&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)  
  
  
