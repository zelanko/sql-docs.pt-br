---
title: Administração de um grupo de disponibilidade (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], managing
ms.assetid: 0b7542fa-235e-413d-81bf-3eff9ee07480
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4896c9219632d816565fdd30c11aa82ccbf7fef1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62791890"
---
# <a name="administration-of-an-availability-group-sql-server"></a>Administração de um grupo de disponibilidade (SQL Server)
  O gerenciamento de um grupo de disponibilidade AlwaysOn existente no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] envolve uma ou mais das seguintes tarefas:  
  
-   Alterar as propriedades de uma réplica de disponibilidade existente, por exemplo, para alterar acesso de conexão de cliente (para configurar réplicas secundárias legíveis), alterar seu modo de failover, modo de disponibilidade ou configuração de tempo limite de sessão.  
  
-   Adicionar ou remover réplicas secundárias.  
  
-   Adicionar ou remover um banco de dados.  
  
-   Suspender ou retomar um banco de dados.  
  
-   Executar um failover manual planejado (um *failover manual*) ou um failover manual forçado (um *failover forçado*).  
  
-   Criar ou configurar um ouvinte de grupo de disponibilidade.  
  
-   Gerenciando [réplicas secundárias legíveis](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md) para um determinado grupo de disponibilidade. Isto envolve a configuração de uma ou mais réplicas para acesso somente leitura ao serem executadas sob a função secundária e configurar o roteamento somente leitura.  
  
-   Gerenciando [backups em réplicas secundárias](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md) para um determinado grupo de disponibilidade. Isto envolve a configuração de onde você prefere que os trabalhos de backup sejam executados e, em seguida, gere scripts de trabalhos de backup para implementar sua preferência de backup. Você precisa gerar script de trabalhos de backup para todos os bancos de dados no grupo de disponibilidade em todas as instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda uma réplica de disponibilidade.  
  
-   Excluir um grupo de disponibilidade.  
  
-   Migração entre clusters de Grupos de Disponibilidade AlwaysOn para atualização do sistema operacional  
  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para configurar um grupo de disponibilidade existente**  
  
-   [Adicionar uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Remover uma réplica secundária de um grupo de disponibilidade &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [Adicionar um banco de dados a um grupo de disponibilidade &#40;SQL Server&#41;](availability-group-add-a-database.md)  
  
-   [Remover um banco de dados secundário de um grupo de disponibilidade &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [Remover um banco de dados primário de um grupo de disponibilidade &#40;SQL Server&#41;](remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
-   [Configurar a política de Failover flexível para controlar condições de Failover automático &#40;grupos de disponibilidade AlwaysOn&#41;](configure-flexible-automatic-failover-policy.md)  
  
 **Para gerenciar um grupo de disponibilidade**  
  
-   [Configurar backup em réplicas de disponibilidade &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [Executar um failover manual planejado de um grupo de disponibilidade &#40;SQL Server&#41;](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [Executar um failover manual forçado de um grupo de disponibilidade &#40;SQL Server&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [Remover um grupo de disponibilidade &#40;SQL Server&#41;](remove-an-availability-group-sql-server.md)  
  
 **Para gerenciar uma réplica de disponibilidade**  
  
-   [Adicionar uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Unir uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Remover uma réplica secundária de um grupo de disponibilidade &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [Alterar o modo de disponibilidade de uma réplica de disponibilidade &#40;SQL Server&#41;](change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [Alterar o modo de failover de uma réplica de disponibilidade &#40;SQL Server&#41;](change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [Configurar backup em réplicas de disponibilidade &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [Configurar o acesso somente leitura em uma réplica de disponibilidade &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Configurar o roteamento somente leitura para um grupo de disponibilidade &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Alterar o período de tempo limite da sessão de uma réplica de disponibilidade &#40;SQL Server&#41;](change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
 **Para gerenciar um banco de dados de disponibilidade**  
  
-   [Adicionar um banco de dados a um grupo de disponibilidade &#40;SQL Server&#41;](availability-group-add-a-database.md)  
  
-   [Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Remover um banco de dados primário de um grupo de disponibilidade &#40;SQL Server&#41;](remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
-   [Remover um banco de dados secundário de um grupo de disponibilidade &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [Suspender um banco de dados de disponibilidade &#40;SQL Server&#41;](suspend-an-availability-database-sql-server.md)  
  
-   [Retomar um banco de dados de disponibilidade &#40;SQL Server&#41;](resume-an-availability-database-sql-server.md)  
  
 **Para monitorar um grupo de disponibilidade**  
  
-   [Monitoramento de grupos de disponibilidade &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)  
  
 **Para dar suporte à migração de grupos de disponibilidade para um novo cluster WSFC (migração entre clusters)**  
  
-   [Alterar o contexto do cluster HADR da instância de servidor &#40;SQL Server&#41;](change-the-hadr-cluster-context-of-server-instance-sql-server.md)  
  
-   [Colocar um grupo de disponibilidade offline &#40;SQL Server&#41;](../../take-an-availability-group-offline-sql-server.md)  
  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   **Blogs:**  
  
     [Blogs da equipe do AlwaysOn do SQL Server: O Team Blog oficial do SQL Server AlwaysOn](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [Blogs dos engenheiros do CSS SQL Server](https://blogs.msdn.com/b/psssql/)  
  
-   **Vídeos:**  
  
     [Microsoft SQL Server codinome "Denali" série AlwaysOn, parte 1: Introducing the Next Generation High Availability Solution](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302) (Série do Always On, codinome "Denali" do Microsoft SQL Server, parte 1: apresentando a próxima geração de solução de alta disponibilidade)  
  
     [Microsoft SQL Server codinome "Denali" série AlwaysOn, parte 2: Criando uma solução de alta disponibilidade de missão crítica usando AlwaysOn](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **White papers:**  
  
     [White papers da Microsoft para SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [White papers da equipe de consultoria do cliente do SQL Server](http://sqlcat.com/)  
  
  
## <a name="see-also"></a>Consulte também  
 [Grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](always-on-availability-groups-sql-server.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Configuração de uma instância de servidor para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](configuration-of-a-server-instance-for-always-on-availability-groups-sql-server.md)  
 [Criação e configuração de grupos de disponibilidade &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)   
 [Secundárias ativas: Réplicas secundárias legíveis &#40;grupos de disponibilidade AlwaysOn&#41;](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [Secundárias ativas: Backup em réplicas secundárias &#40;grupos de disponibilidade AlwaysOn&#41;](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)  
 [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [Políticas AlwaysOn para problemas operacionais com grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](always-on-policies-for-operational-issues-always-on-availability.md)   
 [Monitoramento de grupos de disponibilidade &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)   
 [Grupos de disponibilidade do AlwaysOn: interoperabilidade &#40;SQL Server&#41;](always-on-availability-groups-interoperability-sql-server.md)   
 [Visão geral de instruções Transact-SQL para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](transact-sql-statements-for-always-on-availability-groups.md)   
 [Visão geral dos Cmdlets do PowerShell para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)  
  
  
