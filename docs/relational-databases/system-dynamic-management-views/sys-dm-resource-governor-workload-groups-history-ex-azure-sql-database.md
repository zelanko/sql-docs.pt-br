---
title: sys.dm_resource_governor_workload_groups_history_ex (banco de dados SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_workload_groups_history_ex_TSQL
- sys.dm_resource_governor_workload_groups_history_ex
- dm_resource_governor_workload_groups_history_ex
- dm_resource_governor_workload_groups_history_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_resource_governor_workload_groups_history_ex dynamic management view
author: joesackmsft
ms.author: josack
ms.openlocfilehash: ac776813cb817d1357948091bfc48c981fa8e730
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053261"
---
# <a name="sysdmresourcegovernorworkloadgroupshistoryex-azure-sql-database"></a>sys.dm_resource_governor_workload_groups_history_ex (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Os pools de instantâneo retorna no intervalo de 15 segundos para os últimos 30 minutos do recurso de estatísticas para um banco de dados do SQL Azure.
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**pool_id**| int |ID do pool de recursos. Não permite valor nulo.|
|**group_id**| int |ID do grupo de carga de trabalho. Não permite valor nulo.|
|**name**| nvarchar(256) |Nome do grupo de carga de trabalho. Não permite valor nulo.|
|**snapshot_time**| datetime |Data e hora do instantâneo de estatísticas de grupo de recursos tirado.|
|**duration_ms**| int |Duração entre o instantâneo atual e a anterior.|
|**active_worker_count**| int |Total de funcionários no instantâneo atual.|
|**active_request_count**| int |Conta de solicitação atual. Não permite valor nulo.|
|**active_session_count**| int |Total de sessões Active Directory no instantâneo atual.|
|**total_request_count**| BIGINT |Conta cumulativa de solicitações concluídas no grupo de carga de trabalho. Não permite valor nulo.|
|**delta_request_count**| int |Contagem de solicitações concluídas no grupo de carga de trabalho desde o último instantâneo. Não permite valor nulo.|
|**total_cpu_usage_ms**| BIGINT |Uso cumulativo da CPU, em milissegundos, pelo grupo de carga de trabalho. Não permite valor nulo.|
|**delta_cpu_usage_ms**| int |Uso da CPU em milissegundos desde o último instantâneo. Não permite valor nulo.|
|**delta_cpu_usage_preemptive_ms**| int |Chamadas ao win32 PreEmptive regem por RG de CPU do SQL, desde o último instantâneo.|
|**delta_reads_reduced_memgrant_count**| int |A contagem de concessões de memória que atingiram o limite de tamanho máximo de consulta desde o último instantâneo. Não permite valor nulo.|
|**reads_throttled**| int |Número total de leituras limitado.|
|**delta_reads_queued**| int |O total de leitura lidas enfileiradas desde o último instantâneo. Permite valor nulo. NULL se o grupo de recursos não for administrado para e/s.|
|**delta_reads_issued**| int |O total lidas emitidas desde o último instantâneo. Permite valor nulo. NULL se o grupo de recursos não for administrado para e/s.|
|**delta_reads_completed**| int |O total lidas concluídas desde o último instantâneo. Não permite valor nulo.|
|**delta_read_bytes**| BIGINT |O número total de bytes lidos desde o último instantâneo. Não permite valor nulo.|
|**delta_read_stall_ms**| int |Tempo total (em milissegundos) entre a chegada de e/s de leitura e a conclusão desde o último instantâneo. Não permite valor nulo.|
|**delta_read_stall_queued_ms**| int |Tempo total (em milissegundos) entre a chegada de e/s de leitura e problema desde o último instantâneo. Permite valor nulo. NULL se o grupo de recursos não for administrado para e/s. Delta_read_stall_queued_ms diferente de zero significa que a e/s está sendo afetado pelo RG.|
|**delta_writes_queued**| int |O total SS de gravação enfileiradas desde o último instantâneo. Permite valor nulo. NULL se o grupo de recursos não for administrado para e/s.|
|**delta_writes_issued**| int |O total de gravação emitidas desde o último instantâneo de IOs. Permite valor nulo. NULL se o grupo de recursos não for administrado para e/s.|
|**delta_writes_completed**| int |O total de gravação concluídas desde o último instantâneo de IOs. Não permite valor nulo.|
|**delta_writes_bytes**| BIGINT |O número total de bytes gravados desde o último instantâneo. Não permite valor nulo.|
|**delta_write_stall_ms**| int |Tempo total (em milissegundos) entre a chegada de e/s de gravação e conclusão desde o último instantâneo. Não permite valor nulo.|
|**delta_background_writes**| int |O total de gravações executadas por tarefas em segundo plano, desde o último instantâneo.|
|**delta_background_write_bytes**| BIGINT |O tamanho total de gravação executado por tarefas em segundo plano, desde o último instantâneo, em bytes.|
|**delta_log_bytes_used**| BIGINT |Log usado desde o último instantâneo em bytes.|
|**delta_log_temp_db_bytes_used**| BIGINT |Log do tempdb usado desde o último instantâneo em bytes.|
|**delta_query_optimizations**| BIGINT |A contagem de otimizações de consulta neste grupo de carga de trabalho desde o último instantâneo. Não permite valor nulo.|
|**delta_suboptimal_plan_generations**| BIGINT |A contagem de gerações de planos inferiores ocorridas neste grupo de carga de trabalho devido à pressão de memória desde o último instantâneo. Não permite valor nulo.
|**max_memory_grant_kb**| BIGINT |Máximo de memória concedida para o grupo em KB.|
|**max_request_cpu_msec**| BIGINT |Uso máximo da CPU, em milissegundos, para uma única solicitação. Não permite valor nulo.|
|**max_concurrent_request**| int |Configuração atual do número máximo de solicitações simultâneas. Não permite valor nulo.|
|**max_io**| int |Limite máximo de e/s para o grupo.|
|**max_global_io**| int |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.
|**max_queued_io**| int |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.|
|**max_log_rate_kb**| BIGINT |Taxa de log máximo (-quilobytes por segundo) no nível do grupo de recursos.|
|**max_session**| int |Limite de sessão para o grupo.|
|**max_worker**| int |Limite para o grupo de trabalho.|
|||

## <a name="permissions"></a>Permissões

Este modo de exibição requer a permissão VIEW SERVER STATE.

## <a name="remarks"></a>Comentários

Os usuários podem acessar este modo de exibição de gerenciamento dinâmico para monitorar quase em tempo real de consumo de recursos para o pool de carga de trabalho do usuário, bem como os pools do sistema interno da instância de banco de dados SQL.

> [!IMPORTANT]
> A maioria dos dados apresentados por esta DMV destina-se para consumo interno e está sujeita a alterações.

## <a name="examples"></a>Exemplos

O exemplo a seguir retorna dados de taxa de log máximo e consumo de cada instantâneo por pool de usuário:

```sql
SELECT snapshot_time,
       name,
       max_log_rate_kb,
       delta_log_bytes_used
FROM sys.dm_resource_governor_workload_groups_history_ex
WHERE name LIKE 'User%'
ORDER BY snapshot_time DESC;
```

## <a name="see-also"></a>Consulte também

- [Governança de taxa de log de conversão](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [Limites de recursos DTU do pool Elástico](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools)
- [Limites de recursos do pool Elástico vCore](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools)
