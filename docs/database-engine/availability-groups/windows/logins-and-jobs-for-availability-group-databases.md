---
title: Gerenciar logons de trabalho para bancos de dados em um grupo de disponibilidade
description: Uma descrição de como gerenciar logons para trabalhos que usam bancos de dados participantes de um grupo de disponibilidade Always On.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
helpviewer_keywords:
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], failover
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: d7da14d3-848c-44d4-8e49-d536a1158a61
author: cawrites
ms.author: chadam
ms.openlocfilehash: 59d07b5a3f469e6c25056b47c5ea859dd6e23afc
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584178"
---
# <a name="manage-logins-for-jobs-using-databases-in-an-always-on-availability-group"></a>Gerenciar logons para trabalhos usando bancos de dados em um grupo de disponibilidade Always On
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Você deve manter o mesmo conjunto de logons de usuários e trabalhos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent rotineiramente em todo banco de dados primário de um grupo de disponibilidade AlwaysOn e nos bancos de dados secundários correspondentes. Os logons e trabalhos devem ser reproduzidos em toda instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospede uma réplica de disponibilidade para o grupo de disponibilidade.  
  
-   **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Trabalhos do agente**  
  
     Você precisa copiar manualmente trabalhos relevantes da instância de servidor que hospeda a réplica primária original nas instâncias de servidor que hospedam as réplicas secundárias originais. Para todos os bancos de dados, você precisa adicionar lógica no início de cada trabalho relevante para que o trabalho seja executado somente no banco de dados primário, ou seja, apenas quando a réplica local for a réplica primária do banco de dados.  
  
     As instâncias de servidor que hospedam as réplicas de disponibilidade de um grupo de disponibilidade podem ser configuradas de maneira diferente, com diferentes letras de unidade de fita ou algo assim. Os trabalhos de cada réplica de disponibilidade devem permitir essas diferenças.  
  
     Observe que os trabalhos de backup podem usar a função [sys.fn_hadr_is_preferred_backup_replica](../../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md) para identificar se a réplica local é a preferencial para backups, de acordo com as preferências de backup do grupo de disponibilidade. Os trabalhos de backup criados usando o [Assistente de Plano de Manutenção](../../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md) nativamente usam essa função. Para outros trabalhos de backup, recomendamos o uso dessa função como condição em seus trabalhos de backup, de forma que eles sejam executados apenas na réplica preferencial. Para obter mais informações, consulte [Secundárias ativas: backup em réplicas secundárias &#40;Grupos de Disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md).  
  
-   **Logons**  
  
     Se você estiver usando bancos de dados independentes, poderá configurar usuários independentes nos bancos de dados e, para esses usuários, não precisará criar logons nas instâncias do servidor que hospedam uma réplica secundária. Para um banco de dados de disponibilidade dependente, você precisará criar usuários para os logons nas instâncias do servidor que hospedam as réplicas de disponibilidade. Para obter mais informações, consulte [CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md).  
  
     Se qualquer um dos seus aplicativos usam [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Autenticação ou um logon local do Windows, consulte [Os logons dos aplicativos que usam a autenticação do SQL Server ou Logon local do Windows](../../../database-engine/availability-groups/windows/logins-and-jobs-for-availability-group-databases.md#SSauthentication), mais adiante neste tópico.  
  
    > [!NOTE]  
    >  Um usuário de banco de dados para o qual o logon do SQL Server não está definido ou está definido incorretamente em uma instância do servidor não pode fazer logon na instância. Esse usuário é um *usuário órfão* do banco de dados nessa instância do servidor. Se um usuário se tornar órfão em uma determinada instância de servidor, você poderá configurar os logons de usuários a qualquer momento. Para obter mais informações, consulte [Solução de problemas de usuários órfãos &#40;SQL Server&#41;](../../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md).  
  
-   **Metadados adicionais**  
  
     Os logons e os trabalhos não são as únicas informações que precisam ser recriadas em cada instância de servidor que hospeda uma réplica secundária para determinado grupo de disponibilidade. Por exemplo, talvez você precise recriar parâmetros de configuração de servidor, credenciais, dados criptografados, permissões, configurações de replicação, aplicativos do service broker, gatilhos (em nível de servidor) e assim por diante. Para obter mais informações, consulte [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor &#40;SQL Server&#41;](../../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).  
  
##  <a name="logins-of-applications-that-use-sql-server-authentication-or-a-local-windows-login"></a><a name="SSauthentication"></a> Os logons dos aplicativos que usam a autenticação do SQL Server ou Logon local do Windows  
 Se um aplicativo usar a autenticação do SQL Server ou um logon local do Windows, as SIDs incompatíveis poderão impedir que o logon do aplicativo seja resolvido em uma instância remota do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. As SIDs incompatíveis fazem o logon se tornar um usuário órfão na instância do servidor remoto. Esse problema pode ocorrer quando um aplicativo se conectar a um banco de dados espelhado ou de envio de logs depois de um failover ou a um banco de dados de assinante de replicação que foi inicializado de um backup.  
  
 Para evitar esse problema, recomendamos que você tome medidas preventivas quando configurar esse aplicativo para usar um banco de dados que seja hospedado por uma instância remota do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A prevenção envolve transferir os logons e as senhas da instância local do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para a instância remota do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações sobre como evitar esse problema, confira o artigo 918992 –[Como transferir os logons e senhas entre instâncias do SQL Server](https://support.microsoft.com/kb/918992/)).  
  
> [!NOTE]  
>  Esse problema afeta contas locais do windows em computadores diferentes. No entanto, esse problema não ocorre para contas de domínio porque o SID será o mesmo em cada computador.  
  
 Para obter mais informações, consulte [Usuários órfãos com espelhamento de banco de dados e envio de logs](/archive/blogs/sqlserverfaq/orphaned-users-with-database-mirroring-and-log-shipping) (um blog do mecanismo de banco de dados).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criar um logon](../../../relational-databases/security/authentication-access/create-a-login.md)  
  
-   [Criar um usuário de banco de dados](../../../relational-databases/security/authentication-access/create-a-database-user.md).  
  
-   [Criar um trabalho](../../../ssms/agent/create-a-job.md)  
  
-   [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor &#40;SQL Server&#41;](../../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Bancos de dados independentes](../../../relational-databases/databases/contained-databases.md)   
 [Criar trabalhos](../../../ssms/agent/create-jobs.md)  
  
