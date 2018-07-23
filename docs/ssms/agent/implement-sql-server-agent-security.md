---
title: Implementar a segurança do SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, security
- security [SQL Server Agent], about security
- security [SQL Server Agent]
- security [SQL Server], SQL Server Agent
ms.assetid: d770d35c-c8de-4e00-9a85-7d03f45a0f0d
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 65e30fea2df001d16bc7873fb64b2da594d3dacf
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37987848"
---
# <a name="implement-sql-server-agent-security"></a>Implementar a segurança do SQL Server Agent
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] O Agent permite que o administrador do banco de dados execute cada etapa de trabalho em um contexto de segurança que tem apenas as permissões necessárias para executá-la, as quais são determinadas por um proxy do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. Para definir as permissões para uma etapa de trabalho em particular, crie um proxy com as permissões necessárias e atribua-o à etapa de trabalho. Um proxy pode ser especificado para mais de uma etapa de trabalho. Para etapas de trabalho que requerem as mesmas permissões, use o mesmo proxy.  
  
A seção a seguir explica qual função de banco de dados deve ser concedida aos usuários para que eles possam criar ou executar trabalhos usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
## <a name="granting-access-to-sql-server-agent"></a>Concedendo acesso ao SQL Server Agent  
Para usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent, os usuários devem ser membros de uma ou mais das seguintes funções de banco de dados fixas:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
Essas funções são armazenadas no banco de dados **msdb** . Por padrão, nenhum usuário é membro dessas funções de banco de dados. A associação a essas funções deve ser explicitamente concedida. Usuários que são membros da função de servidor fixa **sysadmin** têm acesso completo ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent e não precisam ser membros dessas funções de banco de dados fixas para usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. Se um usuário não for membro dessas funções de banco de dados fixas ou da função **sysadmin** , o nó do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent não estará disponível quando ele se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].  
  
Os membros dessas funções de banco de dados podem visualizar e executar tarefas de sua propriedade, bem como criar etapas de trabalho executadas como uma conta proxy existente. Para obter mais informações sobre as permissões específicas associadas a cada uma dessas funções de banco de dados fixas do Agent, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
Membros da função de servidor fixa **sysadmin** têm permissão para criar, modificar e excluir contas proxy. Membros da função **sysadmin** têm permissão para criar etapas de trabalho que não especificam um proxy, mas são executadas como a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent, que é a conta usada para iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
## <a name="guidelines"></a>Diretrizes  
Siga estas diretrizes para melhorar a segurança de sua implementação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent:  
  
-   Crie contas de usuário dedicadas especificamente para proxies e utilize somente essas para executar etapas de trabalho.  
  
-   Conceda as permissões necessárias apenas a contas de usuário de proxy. Conceda apenas as permissões realmente necessárias para executar as etapas de trabalho atribuídas a uma determinada conta proxy.  
  
-   Não execute o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent sob uma conta do Microsoft Windows que não seja membro do grupo **Administradores** do Windows.  
  
-   Os proxies são tão seguros quanto o repositório de credencial do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
-   Se as operações de gravação de usuário puderem gravar no log de eventos NT, eles poderão gerar alertas via [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
-   Não especifique a conta de administração NT como uma conta de serviço ou conta proxy.  
  
-   Observe que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent têm acesso aos ativos um do outro. Os dois serviços compartilham um único espaço de processamento e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent é um sysadmin no serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
-   Quando um TSX se inscrever com um MSX, o sysadmins do MSX obtém controle total sobre a instância de TSX do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   ACE é uma extensão e não pode se chamar. ACE é chamado por Chainer ScenarioEngine.exe, também conhecido como Microsoft.SqlServer.Chainer.Setup.exe, ou pode ser chamado por outro processo do host.  
  
-   ACE depende das seguintes DLLs de configuração de propriedade do SSDP, porque essas APIs de DLLs são chamadas pelo ACE:  
  
    -   **SCO** – Microsoft.SqlServer.Configuration.Sco.dll, incluindo novas validações de SCO para contas virtuais  
  
    -   **Cluster** – Microsoft.SqlServer.Configuration.Cluster.dll  
  
    -   **SFC** – Microsoft.SqlServer.Configuration.SqlConfigBase.dll  
  
    -   **Extensão** – Microsoft.SqlServer.Configuration.ConfigExtension.dll  
  
## <a name="see-also"></a>Consulte Também  
[Usando funções predefinidas](http://msdn.microsoft.com/en-us/6b46db51-7c30-467d-a251-50f50647fe21)  
[sp_addrolemember (Transact-SQL)](http://msdn.microsoft.com/en-us/a583c087-bdb3-46d2-b9e5-3921b3e6d10b)  
[sp_droprolemember (Transact-SQL)](http://msdn.microsoft.com/en-us/c2f19ab1-e742-4d56-ba8e-8ffd40cf4925)  
[Segurança e proteção (Mecanismo de Banco de Dados)](http://msdn.microsoft.com/en-us/dfb39d16-722a-4734-94bb-98e61e014ee7)  
  
