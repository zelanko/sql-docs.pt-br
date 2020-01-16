---
title: Exibir propriedades do grupo de disponibilidade
description: 'Exiba as propriedades de um grupo de disponibilidade Always On com SSMS (SQL Server Management Studio), T-SQL (Transact-SQL) ou SQL PowerShell. '
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server]
ms.assetid: 61243c87-bd62-4510-863f-2a8f347caf1f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 44328d275c962c1f6315e56e763c3a8550318ffb
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2019
ms.locfileid: "74821815"
---
# <a name="view-availability-group-properties-sql-server"></a>Exibir propriedades do grupo de disponibilidade (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como exibir as propriedades de um grupo de disponibilidade AlwaysOn usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)] no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para exibir e alterar as propriedades de um grupo de disponibilidade**  
  
1.  No Pesquisador de Objetos, conecte-se à instância de servidor que hospeda a réplica primária e expanda a árvore de servidores.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade**.  
  
3.  Clique com o botão direito do mouse no grupo de disponibilidade cujas propriedades você deseja exibir e selecione o comando **Propriedades** .  
  
4.  Na caixa de diálogo **Propriedades do Grupo de disponibilidade** , use as páginas **Geral** e **Preferências de Backup** para exibir e, em alguns casos, alterar as propriedades do grupo de disponibilidade selecionado. Para obter mais informações, confira [Propriedades do Grupo de Disponibilidade: novo grupo de disponibilidade &#40;Página Geral&#41;](../../../database-engine/availability-groups/windows/availability-group-properties-new-availability-group-general-page.md) e [Propriedades do grupo de disponibilidade: novo grupo de disponibilidade &#40;página Preferências de Backup&#41;](../../../database-engine/availability-groups/windows/availability-group-properties-new-availability-group-backup-preferences-page.md).  
  
     Use a página **Permissões** para exibir os logons, funções e permissões explícitas atuais associados ao grupo de disponibilidade. Para obter mais informações, consulte [Permissions or Securables Page](../../../relational-databases/security/permissions-or-securables-page.md).  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para exibir as propriedades e o estado de um grupo de disponibilidade**  
  
 Para consultar as propriedades e os estados de grupos de disponibilidade para os quais a instância do servidor hospeda uma réplica de disponibilidade, use as exibições a seguir:  
  
 [sys.availability_groups](../../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)  
 Retorna uma linha para cada grupo de disponibilidade para o qual a instância local do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] hospeda uma réplica de disponibilidade. Cada linha contém uma cópia armazenada em cache dos metadados do grupo de disponibilidade.  
  
 **Nomes de colunas:** group_id, name, resource_id, resource_group_id, failure_condition_level, health_check_timeout, automated_backup_preference, automated_backup_preference_desc  
  
 [sys.availability_groups_cluster](../../../relational-databases/system-catalog-views/sys-availability-groups-cluster-transact-sql.md)  
 Retorna uma linha para cada grupo de disponibilidade no cluster do WSFC. Cada linha contém os metadados do grupo de disponibilidade do cluster do WSFC (Windows Server Failover Clustering).  
  
 **Nomes de colunas:** group_id, name, resource_id, resource_group_id, failure_condition_level, health_check_timeout, automated_backup_preference, automated_backup_preference_desc  
  
 [sys.dm_hadr_availability_group_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql.md)  
 Retorna uma linha para cada grupo de disponibilidade que possui uma réplica de disponibilidade na instância local do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Cada linha exibe os estados que definem a integridade de um determinado grupo de disponibilidade.  
  
 **Nomes de colunas:** group_id, primary_replica, primary_recovery_health, primary_recovery_health_desc, secondary_recovery_health, secondary_recovery_health_desc, synchronization_health, synchronization_health_desc  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para exibir informações sobre os grupos de disponibilidade**  
  
-   [Exibir as propriedades da réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-replica-properties-sql-server.md)  
  
-   [Exibir propriedades do ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)  
  
-   [Políticas AlwaysOn para problemas operacionais com grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md)  
  
-   [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
-   [Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
 **Para configurar um grupo de disponibilidade existente**  
  
-   [Adicionar uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Remover uma réplica secundária de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [Adicionar um banco de dados a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/availability-group-add-a-database.md)  
  
-   [Remover um banco de dados secundário de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Remover um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-listener-sql-server.md)  
  
-   [Remover um banco de dados primário de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
-   [Remover um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)  
  
 **Para fazer o failover de um grupo de disponibilidade manualmente**  
  
-   [Executar um failover manual planejado de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [Executar um failover manual forçado de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Políticas AlwaysOn para problemas operacionais com grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md)  
  
  
