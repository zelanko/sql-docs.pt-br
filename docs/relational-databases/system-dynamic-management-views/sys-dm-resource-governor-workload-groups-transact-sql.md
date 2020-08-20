---
description: sys.dm_resource_governor_workload_groups (Transact-SQL)
title: sys. dm_resource_governor_workload_groups (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2020
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dfcbcaceeb4e60a88f1ba00fa7a116629945c7e5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454871"
---
# <a name="sysdm_resource_governor_workload_groups-transact-sql"></a>sys.dm_resource_governor_workload_groups (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna as estatísticas de grupo de carga de trabalho e configuração na memória atual do grupo de carga de trabalho. Esta exibição pode ser unida a sys.dm_resource_governor_resource_pools para obter o nome do pool de recursos.  
  
> [!NOTE]  
>  Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use o nome **Sys. dm_pdw_nodes_resource_governor_workload_groups**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|group_id|**int**|ID do grupo de carga de trabalho. Não permite valor nulo.|  
|name|**sysname**|Nome do grupo de carga de trabalho. Não permite valor nulo.|  
|pool_id|**int**|ID do pool de recursos. Não permite valor nulo.|  
|external_pool_id|**int**|**Aplica-se a: a**partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] .<br /><br /> ID do pool de recursos externos. Não permite valor nulo.|  
|statistics_start_time|**datetime**|Hora em que coleta de estatísticas foi redefinida para o grupo de carga de trabalho. Não permite valor nulo.|  
|total_request_count|**bigint**|Conta cumulativa de solicitações concluídas no grupo de carga de trabalho. Não permite valor nulo.|  
|total_queued_request_count|**bigint**|Conta cumulativa de solicitações em fila depois que o limite de GROUP_MAX_REQUESTS foi alcançado. Não permite valor nulo.|  
|active_request_count|**int**|Conta de solicitação atual. Não permite valor nulo.|  
|queued_request_count|**int**|Conta de solicitação em fila atual. Não permite valor nulo.|  
|total_cpu_limit_violation_count|**bigint**|Conta cumulativa de solicitações que excedem o limite de CPU. Não permite valor nulo.|  
|total_cpu_usage_ms|**bigint**|Uso cumulativo da CPU, em milissegundos, pelo grupo de carga de trabalho. Não permite valor nulo.|  
|max_request_cpu_time_ms|**bigint**|Uso máximo da CPU, em milissegundos, para uma única solicitação. Não permite valor nulo.<br /><br /> **Observação:** Esse é um valor medido, ao contrário de request_max_cpu_time_sec, que é uma configuração configurável. Para obter mais informações, consulte [Classe de evento CPU Threshold Exceeded](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md).|  
|blocked_task_count|**int**|Contagem atual de tarefas bloqueadas. Não permite valor nulo.|  
|total_lock_wait_count|**bigint**|Contagem cumulativa de esperas de bloqueio ocorridas. Não permite valor nulo.|  
|total_lock_wait_time_ms|**bigint**|Soma cumulativa de tempo, em milissegundos, em que um bloqueio é mantido. Não permite valor nulo.|  
|total_query_optimization_count|**bigint**|Contagem cumulativa de otimizações de consulta neste grupo de carga de trabalho. Não permite valor nulo.|  
|total_suboptimal_plan_generation_count|**bigint**|Conta cumulativa de gerações de planos inferiores ocorridas neste grupo de carga de trabalho devido à pressão de memória. Não permite valor nulo.|  
|total_reduced_memgrant_count|**bigint**|Contagem cumulativa de concessões de memória que alcançaram o limite de tamanho de consulta máximo. Não permite valor nulo.|  
|max_request_grant_memory_kb|**bigint**|Tamanho máximo de memória concedida, em quilobytes, de uma única solicitação desde que as estatísticas foram redefinidas. Não permite valor nulo.|  
|active_parallel_thread_count|**bigint**|Contagem atual de uso de threads paralelos. Não permite valor nulo.|  
|importance|**sysname**|Valor de configuração atual para a importância relativa de uma solicitação neste grupo de carga de trabalho. A importância é um dos seguintes, sendo que médio é o padrão: baixo, médio ou alto.<br /><br /> Não permite valor nulo.|  
|request_max_memory_grant_percent|**int**|Configuração atual da concessão de memória máxima, como uma porcentagem, para uma única solicitação. Não permite valor nulo.|  
|request_max_cpu_time_sec|**int**|Configuração atual de limite máximo de uso da CPU, em segundos, de uma única solicitação. Não permite valor nulo.|  
|request_memory_grant_timeout_sec|**int**|Configuração atual do tempo limite de concessão de memória, em segundos, de uma única solicitação. Não permite valor nulo.|  
|group_max_requests|**int**|Configuração atual do número máximo de solicitações simultâneas. Não permite valor nulo.|  
|max_dop|**int**|Grau máximo de paralelismo configurado para o grupo de carga de trabalho. O valor padrão, 0, usa configurações globais. Não permite valor nulo.| 
|effective_max_dop|**int**|**Aplica-se a: a**partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] .<br /><br />Grau máximo de paralelismo efetivo para o grupo de carga de trabalho. Não permite valor nulo.| 
|total_cpu_usage_preemptive_ms|**bigint**|**Aplica-se a: a**partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] .<br /><br />Tempo total de CPU usado durante o agendamento do modo preemptivo para o grupo de carga de trabalho, medido em MS. Não permite valor nulo.<br /><br />Para executar código fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (por exemplo, procedimentos armazenados estendidos e consultas distribuídas), um thread deve ser executado fora do controle de um agendador não preventivo. Para fazer isso, um trabalhador muda para o modo preventivo.| 
|request_max_memory_grant_percent_numeric|**float**|**Aplica-se a: a**partir de [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] .<br /><br />Configuração atual da concessão de memória máxima, como uma porcentagem, para uma única solicitação. Não permite valor nulo.| 
|pdw_node_id|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="remarks"></a>Comentários  
 Essa exibição de gerenciamento dinâmico mostra a configuração na memória. Para ver os metadados de configuração armazenados, use a exibição de catálogo de [&#41;de &#40;resource_governor_workload_groups do Transact-SQL ](../../relational-databases/system-catalog-views/sys-resource-governor-workload-groups-transact-sql.md) .  
  
 Quando `ALTER RESOURCE GOVERNOR RESET STATISTICS` é executado com êxito, os seguintes contadores são redefinidos:,,,,,,,, `statistics_start_time` `total_request_count` ,, `total_queued_request_count` `total_cpu_limit_violation_count` `total_cpu_usage_ms` `max_request_cpu_time_ms` `total_lock_wait_count` `total_lock_wait_time_ms` `total_query_optimization_count` `total_suboptimal_plan_generation_count` `total_reduced_memgrant_count` e `max_request_grant_memory_kb` . O contador `statistics_start_time` é definido como a data e hora atuais do sistema e os outros contadores são definidos como zero (0).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão `VIEW SERVER STATE`.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys. dm_resource_governor_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)   
 [sys. resource_governor_workload_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-workload-groups-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
