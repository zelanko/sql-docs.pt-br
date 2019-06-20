---
title: Implementar a segurança do SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, security
- security [SQL Server Agent], about security
- security [SQL Server Agent]
- security [SQL Server], SQL Server Agent
ms.assetid: d770d35c-c8de-4e00-9a85-7d03f45a0f0d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 52537ac126115fbde3d7d0fb1a13f61f1d25cf15
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63137525"
---
# <a name="implement-sql-server-agent-security"></a>Implementar a segurança do SQL Server Agent
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent permite que o administrador do banco de dados execute cada etapa de trabalho em um contexto de segurança que tem apenas as permissões necessárias para executá-la, as quais são determinadas por um proxy do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Para definir as permissões para uma etapa de trabalho em particular, crie um proxy com as permissões necessárias e atribua-o à etapa de trabalho. Um proxy pode ser especificado para mais de uma etapa de trabalho. Para etapas de trabalho que requerem as mesmas permissões, use o mesmo proxy.  
  
 A seção a seguir explica qual função de banco de dados deve ser concedida aos usuários para que eles possam criar ou executar trabalhos usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="granting-access-to-sql-server-agent"></a>Concedendo acesso ao SQL Server Agent  
 Para usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, os usuários devem ser membros de uma ou mais das seguintes funções de banco de dados fixas:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Essas funções são armazenadas no banco de dados **msdb** . Por padrão, nenhum usuário é membro dessas funções de banco de dados. A associação a essas funções deve ser explicitamente concedida. Usuários que são membros da função de servidor fixa **sysadmin** têm acesso completo ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e não precisam ser membros dessas funções de banco de dados fixas para usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Se um usuário não for membro dessas funções de banco de dados fixas ou da função **sysadmin** , o nó do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não estará disponível quando ele se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Os membros dessas funções de banco de dados podem visualizar e executar tarefas de sua propriedade, bem como criar etapas de trabalho executadas como uma conta proxy existente. Para obter mais informações sobre as permissões específicas associadas a cada uma dessas funções de banco de dados fixas do Agent, consulte [Funções de banco de dados fixas do SQL Server Agent](sql-server-agent-fixed-database-roles.md).  
  
 Membros da função de servidor fixa **sysadmin** têm permissão para criar, modificar e excluir contas proxy. Membros da função **sysadmin** têm permissão para criar etapas de trabalho que não especificam um proxy, mas são executadas como a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, que é a conta usada para iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="guidelines"></a>Diretrizes  
 Siga estas diretrizes para melhorar a segurança de sua implementação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent:  
  
-   Crie contas de usuário dedicadas especificamente para proxies e utilize somente essas para executar etapas de trabalho.  
  
-   Conceda as permissões necessárias apenas a contas de usuário de proxy. Conceda apenas as permissões realmente necessárias para executar as etapas de trabalho atribuídas a uma determinada conta proxy.  
  
-   Não execute o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sob uma conta do Microsoft Windows que não seja membro do grupo **Administradores** do Windows.  
  
-   Os proxies são tão seguros quanto o repositório de credencial do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Se as operações de gravação de usuário puderem gravar no log de eventos NT, eles poderão gerar alertas via [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
-   Não especifique a conta de administração NT como uma conta de serviço ou conta proxy.  
  
-   Observe que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent têm acesso aos ativos um do outro. Os dois serviços compartilham um único espaço de processamento e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é um sysadmin no serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Quando um TSX se inscrever com um MSX, o sysadmins do MSX obtém controle total sobre a instância de TSX do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   ACE é uma extensão e não pode se chamar. ACE é chamado por Chainer ScenarioEngine.exe (também conhecido como Microsoft.SqlServer.Chainer.Setup.exe) ou pode ser chamado por outro processo do host.  
  
-   ACE depende das seguintes DLLs de configuração de propriedade do SSDP, porque essas APIs de DLLs são chamadas pelo ACE:  
  
    -   **SCO** – Microsoft.SqlServer.Configuration.Sco.dll, incluindo novas validações de SCO para contas virtuais  
  
    -   **Cluster** – Microsoft.SqlServer.Configuration.Cluster.dll  
  
    -   **SFC** – Microsoft.SqlServer.Configuration.SqlConfigBase.dll  
  
    -   **Extensão** – Microsoft.SqlServer.Configuration.ConfigExtension.dll  
  
## <a name="see-also"></a>Consulte também  
 [funções predefinidas](../../reporting-services/security/role-definitions-predefined-roles.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql)   
 [sp_droprolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql)   
 [Central de segurança do Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
