---
description: sys.dm_resource_governor_workload_groups_history_ex (Banco de Dados SQL do Azure)
title: sys.dm_resource_governor_workload_groups_history_ex (banco de dados SQL do Azure) | Microsoft Docs
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
ms.openlocfilehash: d761d1ca80037e26f8757ec681929dd5356b182f
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/08/2020
ms.locfileid: "91834400"
---
# <a name="sysdm_resource_governor_workload_groups_history_ex-azure-sql-database"></a>sys.dm_resource_governor_workload_groups_history_ex (Banco de Dados SQL do Azure)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

Retorna o instantâneo a um intervalo de 20 segundos para os últimos 32 minutos (128 segundos no total) de estatísticas de pools de recursos para um banco de dados SQL do Azure.
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**pool_id**| INT |ID do pool de recursos. Não permite valor nulo.|
|**group_id**| INT |ID do grupo de carga de trabalho. Não permite valor nulo.|
|**name**| nvarchar(256) |Nome do grupo de carga de trabalho. Não permite valor nulo.|
|**snapshot_time**| DATETIME |DateTime do instantâneo de estatísticas do grupo de recursos feito.|
|**duration_ms**| INT |Duração entre o instantâneo atual e o anterior.|
|**active_worker_count**| INT |Total de trabalhos no instantâneo atual.|
|**active_request_count**| INT |Conta de solicitação atual. Não permite valor nulo.|
|**active_session_count**| INT |Total de sessões ativas no instantâneo atual.|
|**total_request_count**| BIGINT |Conta cumulativa de solicitações concluídas no grupo de carga de trabalho. Não permite valor nulo.|
|**delta_request_count**| INT |Contagem de solicitações concluídas no grupo de cargas de trabalho desde o último instantâneo. Não permite valor nulo.|
|**total_cpu_usage_ms**| BIGINT |Uso cumulativo da CPU, em milissegundos, pelo grupo de carga de trabalho. Não permite valor nulo.|
|**delta_cpu_usage_ms**| INT |Uso da CPU em milissegundos desde o último instantâneo. Não permite valor nulo.|
|**delta_cpu_usage_preemptive_ms**| INT |As chamadas do Win32 preemptivas não são regidas pelo RG da CPU do SQL, desde o último instantâneo.|
|**delta_reads_reduced_memgrant_count**| INT |A contagem de concessões de memória que atingiu o limite máximo de tamanho de consulta desde o último instantâneo. Não permite valor nulo.|
|**reads_throttled**| INT |Número total de leituras limitadas.|
|**delta_reads_queued**| INT |O IOs de leitura total enfileirado desde o último instantâneo. Permite valor nulo. NULL se o grupo de recursos não for regido para e/s.|
|**delta_reads_issued**| INT |O IOs de leitura total emitido desde o último instantâneo. Permite valor nulo. NULL se o grupo de recursos não for regido para e/s.|
|**delta_reads_completed**| INT |O IOs de leitura total foi concluído desde o último instantâneo. Não permite valor nulo.|
|**delta_read_bytes**| BIGINT |O número total de bytes lidos desde o último instantâneo. Não permite valor nulo.|
|**delta_read_stall_ms**| INT |Tempo total (em milissegundos) entre a chegada de e/s de leitura e a conclusão desde o último instantâneo. Não permite valor nulo.|
|**delta_read_stall_queued_ms**| INT |Tempo total (em milissegundos) entre a chegada de e/s de leitura e o problema desde o último instantâneo. Permite valor nulo. NULL se o grupo de recursos não for regido para e/s. Delta_read_stall_queued_ms diferente de zero significa que a e/s está sendo afetada pelo RG.|
|**delta_writes_queued**| INT |O IOs de gravação total enfileirado desde o último instantâneo. Permite valor nulo. NULL se o grupo de recursos não for regido para e/s.|
|**delta_writes_issued**| INT |O IOs de gravação total emitido desde o último instantâneo. Permite valor nulo. NULL se o grupo de recursos não for regido para e/s.|
|**delta_writes_completed**| INT |O IOs de gravação total foi concluído desde o último instantâneo. Não permite valor nulo.|
|**delta_writes_bytes**| BIGINT |O número total de bytes gravados desde o último instantâneo. Não permite valor nulo.|
|**delta_write_stall_ms**| INT |Tempo total (em milissegundos) entre a chegada de e/s de gravação e a conclusão desde o último instantâneo. Não permite valor nulo.|
|**delta_background_writes**| INT |O total de gravações realizadas por tarefas em segundo plano desde o último instantâneo.|
|**delta_background_write_bytes**| BIGINT |O tamanho total de gravação realizado pelas tarefas em segundo plano desde o último instantâneo, em bytes.|
|**delta_log_bytes_used**| BIGINT |Log usado desde o último instantâneo em bytes.|
|**delta_log_temp_db_bytes_used**| BIGINT |Log de tempdb usado desde o último instantâneo em bytes.|
|**delta_query_optimizations**| BIGINT |A contagem de otimizações de consulta neste grupo de carga de trabalho desde o último instantâneo. Não permite valor nulo.|
|**delta_suboptimal_plan_generations**| BIGINT |A contagem de gerações de planos de qualidade inferior ocorridas neste grupo de cargas de trabalho devido à pressão de memória desde o último instantâneo. Não permite valor nulo.
|**max_memory_grant_kb**| BIGINT |Concessão máxima de memória para o grupo em KB.|
|**max_request_cpu_msec**| BIGINT |Uso máximo da CPU, em milissegundos, para uma única solicitação. Não permite valor nulo.|
|**max_concurrent_request**| INT |Configuração atual do número máximo de solicitações simultâneas. Não permite valor nulo.|
|**max_io**| INT |Limite máximo de e/s para o grupo.|
|**max_global_io**| INT |Identificado apenas para fins informativos. Não há suporte. A compatibilidade futura não está garantida.
|**max_queued_io**| INT |Identificado apenas para fins informativos. Não há suporte. A compatibilidade futura não está garantida.|
|**max_log_rate_kb**| BIGINT |Taxa máxima de log (quilobytes-bytes por segundo) em nível de grupo de recursos.|
|**max_session**| INT |Limite de sessão do grupo.|
|**max_worker**| INT |Limite de trabalho para o grupo.|
|||

## <a name="permissions"></a>Permissões

Esta exibição requer a permissão VIEW SERVER STATE.

## <a name="remarks"></a>Comentários

Os usuários podem acessar essa exibição de gerenciamento dinâmico para monitorar o consumo de recursos quase em tempo real para o pool de carga de trabalho do usuário, bem como os pools internos do sistema da instância do banco de dados SQL

> [!IMPORTANT]
> A maioria dos dados exibidos por essa DMV destina-se ao consumo interno e está sujeita a alterações.

## <a name="examples"></a>Exemplos

O exemplo a seguir retorna dados de taxa de log máximos e consumo em cada instantâneo pelo pool de usuários:

```sql
SELECT snapshot_time,
       name,
       max_log_rate_kb,
       delta_log_bytes_used
FROM sys.dm_resource_governor_workload_groups_history_ex
WHERE name LIKE 'User%'
ORDER BY snapshot_time DESC;
```

## <a name="see-also"></a>Consulte Também

- [Governança de taxa de log de tradução](/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [Limites de recursos DTU do pool elástico](/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools)
- [Limites de recursos vCore do pool elástico](/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools)