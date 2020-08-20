---
description: sys.dm_hadr_database_replica_cluster_states (Transact-SQL)
title: sys. dm_hadr_database_replica_cluster_states (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_database_replica_cluster_states
- dm_hadr_database_replica_cluster_states_TSQL
- sys.dm_hadr_database_replica_cluster_states_TSQL
- dm_hadr_database_replica_cluster_states
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_database_replica_cluster_states dynamic management view
ms.assetid: 6f719071-ebce-470d-aebd-1f55ee8cd70a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6e12ac1d979d1acfab0614bad27ae2f937245870
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489830"
---
# <a name="sysdm_hadr_database_replica_cluster_states-transact-sql"></a>sys.dm_hadr_database_replica_cluster_states (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha que contém informações destinadas a fornecer uma visão da integridade dos bancos de dados de disponibilidade nos grupos de disponibilidade Always On em cada grupo de disponibilidade Always On no cluster do WSFC (Windows Server Failover Clustering). Consulte **Sys. dm_hadr_database_replica_states** para responder às seguintes perguntas:  
  
-   Todos os bancos de dados estão em um grupo de disponibilidade pronto para um failover?  
  
-   Depois de um failover forçado, um banco de dados secundário se suspendeu localmente e confirmou seu estado suspenso para a nova réplica primária?  
  
-   Se a réplica primária estiver indisponível no momento, qual réplica secundária permitirá a perda de dados mínima caso se torne a réplica primária?  
  
-   Quando o valor da coluna [Sys. databases](~/relational-databases/system-catalog-views/sys-databases-transact-sql.md)   **log_reuse_wait_desc** é "AVAILABILITY_REPLICA", qual réplica secundária em um grupo de disponibilidade está mantendo o truncamento de log em um determinado banco de dados primário?  
   
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|O identificador da réplica de disponibilidade dentro do grupo de disponibilidade.|  
|**group_database_id**|**uniqueidentifier**|O identificador do banco de dados dentro do grupo de disponibilidade. Esse identificador é idêntico em cada réplica à qual este banco de dados é unido.|  
|**database_name**|**sysname**|Nome de um banco de dados que pertence ao grupo de disponibilidade.|  
|**is_failover_ready**|**bit**|Indica se o banco de dados secundário está sincronizado com o banco de dados primário correspondente. um dos:<br /><br /> 0 = O banco de dados não está marcado como sincronizado no cluster. O banco de dados não está pronto para um failover.<br /><br /> 1 = O banco de dados está marcado como sincronizado no cluster. O banco de dados está pronto para um failover.|  
|**is_pending_secondary_suspend**|**bit**|Indica se, depois de um failover forçado, o banco de dados tem suspensão pendente, um dos seguintes:<br /><br /> 0 = Qualquer estado com exceção de HADR_SYNCHRONIZED_ SUSPENDED.<br /><br /> 1 = HADR_SYNCHRONIZED_ SUSPENDED. Quando um failover forçado é concluído, cada um dos bancos de dados secundários é definido como HADR_SYNCHONIZED_SUSPENDED e permanece nesse estado até que a nova réplica primária receba uma confirmação daquele banco de dados secundário para a mensagem de SUSPEND.<br /><br /> NULL = Desconhecido (sem quorum)|  
|**is_database_joined**|**bit**|Indica se o banco de dados nesta réplica de disponibilidade foi unido ao grupo de disponibilidade, um do seguintes:<br /><br /> 0 = O banco de dados não está unido ao grupo de disponibilidade nesta réplica de disponibilidade.<br /><br /> 1 = O banco de dados está unido ao grupo de disponibilidade nesta réplica de disponibilidade.<br /><br /> NULL = desconhecido (a réplica de disponibilidade não tem quorum).|  
|**recovery_lsn**|**numeric(25,0)**|Na réplica primária, o final do log de transações antes de a réplica gravar outro novo registro de log depois da recuperação ou do failover. Na réplica primária, a linha de um determinado banco de dados secundário terá o valor para o qual a réplica primária precisa da réplica secundária com a qual sincronizar (isto é, reverter para e reinicializar para).<br /><br /> Em réplicas secundárias esse valor é NULL. Observe que cada réplica secundária terá o valor MAX ou um valor inferior, para o qual a réplica primária informou à réplica secundária para retornar.|  
|**truncation_lsn**|**numeric(25,0)**|O valor de truncamento de log do [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], que poderá ser mais alto que o LSN de truncamento local se o truncamento de log local for bloqueado (como por uma operação de backup).|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Always On funções e exibições de gerenciamento dinâmico de grupos de disponibilidade &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Exibições de catálogo de grupos de disponibilidade AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Monitorar grupos de disponibilidade &#40;&#41;Transact-SQL ](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [sys.dm_hadr_database_replica_states &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)  
  
  
