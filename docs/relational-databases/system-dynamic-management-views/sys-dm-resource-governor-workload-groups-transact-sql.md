---
title: sys.dm_resource_governor_workload_groups (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/30/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_workload_groups
- sys.dm_resource_governor_workload_groups_TSQL
- dm_resource_governor_workload_groups
- dm_resource_governor_workload_groups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_resource_governor_workload_groups dynamic management view
ms.assetid: f63c4914-1272-43ef-b135-fe1aabd953e0
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 588bbcb915873ba8a121432a83579b5877df8454
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmresourcegovernorworkloadgroups-transact-sql"></a>sys.dm_resource_governor_workload_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Retorna as estatísticas de grupo de carga de trabalho e configuração na memória atual do grupo de carga de trabalho. Esta exibição pode ser unida a sys.dm_resource_governor_resource_pools para obter o nome do pool de recursos.  
  
> [!NOTE]  
>  Para chamar essa de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_resource_governor_workload_groups**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|group_id|**Int**|ID do grupo de carga de trabalho. Não permite valor nulo.|  
|name|**sysname**|Nome do grupo de carga de trabalho. Não permite valor nulo.|  
|pool_id|**Int**|ID do pool de recursos. Não permite valor nulo.|  
|external_pool_id|**Int**|**Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> ID do pool de recursos externos. Não permite valor nulo.|  
|statistics_start_time|**datetime**|Hora em que coleta de estatísticas foi redefinida para o grupo de carga de trabalho. Não permite valor nulo.|  
|total_request_count|**bigint**|Conta cumulativa de solicitações concluídas no grupo de carga de trabalho. Não permite valor nulo.|  
|total_queued_request_count|**bigint**|Conta cumulativa de solicitações em fila depois que o limite de GROUP_MAX_REQUESTS foi alcançado. Não permite valor nulo.|  
|active_request_count|**Int**|Conta de solicitação atual. Não permite valor nulo.|  
|queued_request_count|**Int**|Conta de solicitação em fila atual. Não permite valor nulo.|  
|total_cpu_limit_violation_count|**bigint**|Conta cumulativa de solicitações que excedem o limite de CPU. Não permite valor nulo.|  
|total_cpu_usage_ms|**bigint**|Uso cumulativo da CPU, em milissegundos, pelo grupo de carga de trabalho. Não permite valor nulo.|  
|max_request_cpu_time_ms|**bigint**|Uso máximo da CPU, em milissegundos, para uma única solicitação. Não permite valor nulo.<br /><br /> **Observação:** isso é um valor medido, ao contrário de request_max_cpu_time_sec, que é uma definição configurável. Para obter mais informações, consulte [limite de CPU excedido classe de evento](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md).|  
|blocked_task_count|**Int**|Contagem atual de tarefas bloqueadas. Não permite valor nulo.|  
|total_lock_wait_count|**bigint**|Contagem cumulativa de esperas de bloqueio ocorridas. Não permite valor nulo.|  
|total_lock_wait_time_ms|**bigint**|Soma cumulativa de tempo, em milissegundos, em que um bloqueio é mantido. Não permite valor nulo.|  
|total_query_optimization_count|**bigint**|Contagem cumulativa de otimizações de consulta neste grupo de carga de trabalho. Não permite valor nulo.|  
|total_suboptimal_plan_generation_count|**bigint**|Conta cumulativa de gerações de planos inferiores ocorridas neste grupo de carga de trabalho devido à pressão de memória. Não permite valor nulo.|  
|total_reduced_memgrant_count|**bigint**|Contagem cumulativa de concessões de memória que alcançaram o limite de tamanho de consulta máximo. Não permite valor nulo.|  
|max_request_grant_memory_kb|**bigint**|Tamanho máximo de memória concedida, em quilobytes, de uma única solicitação desde que as estatísticas foram redefinidas. Não permite valor nulo.|  
|active_parallel_thread_count|**bigint**|Contagem atual de uso de threads paralelos. Não permite valor nulo.|  
|importance|**sysname**|Valor de configuração atual para a importância relativa de uma solicitação neste grupo de carga de trabalho. A importância é uma das seguintes opções, com Medium sendo o padrão: alta, média ou baixa.<br /><br /> Não permite valor nulo.|  
|request_max_memory_grant_percent|**Int**|Configuração atual da concessão de memória máxima, como uma porcentagem, para uma única solicitação. Não permite valor nulo.|  
|request_max_cpu_time_sec|**Int**|Configuração atual de limite máximo de uso da CPU, em segundos, de uma única solicitação. Não permite valor nulo.|  
|request_memory_grant_timeout_sec|**Int**|Configuração atual do tempo limite de concessão de memória, em segundos, de uma única solicitação. Não permite valor nulo.|  
|group_max_requests|**Int**|Configuração atual do número máximo de solicitações simultâneas. Não permite valor nulo.|  
|max_dop|**Int**|Grau máximo de paralelismo para o grupo de carga de trabalho. O valor padrão, 0, usa configurações globais. Não permite valor nulo.|  
|pdw_node_id|**Int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="remarks"></a>Remarks  
 Essa exibição de gerenciamento dinâmico mostra a configuração na memória. Para consultar os metadados de configuração armazenada, use a exibição de catálogo sys.resource_governor_workload_groups.  
  
 Quando ALTER RESOURCE GOVERNOR RESET STATISTICS é executado com êxito, os seguintes contadores são redefinidos: statistics_start_time, total_request_count, total_queued_request_count, total_cpu_limit_violation_count, total_cpu_usage_ms, max_request_ cpu_time_ms, total_lock_wait_count, total_lock_wait_time_ms, total_query_optimization_count, total_suboptimal_plan_generation_count, total_reduced_memgrant_count e max_request_grant_memory_kb. statistics_start_time é definido como a data atual do sistema e a hora, os outros contadores são definidos como zero (0).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW SERVER STAT.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys.dm_resource_governor_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)   
 [sys.resource_governor_workload_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-workload-groups-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  



