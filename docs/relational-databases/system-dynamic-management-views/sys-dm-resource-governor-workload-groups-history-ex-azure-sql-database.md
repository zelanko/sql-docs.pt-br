---
title: sys. dm _resource_governor_workload_groups_history_ex (banco de dados SQL do Azure) | Microsoft Docs
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
ms.openlocfilehash: 5fea5badf14ce9863f07dff189f1665788ec5fb6
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70873773"
---
# <a name="sysdm_resource_governor_workload_groups_history_ex-azure-sql-database"></a>sys.dm_resource_governor_workload_groups_history_ex (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Retorna o instantâneo em um intervalo de 20 segundos para os últimos 32 minutos (128 Recs no total) de estatísticas de pools de recursos para um banco de dados SQL do Azure.
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**pool_id**| int |ID do pool de recursos. Não permite valor nulo.|
|**group_id**| int |ID do grupo de carga de trabalho. Não permite valor nulo.|
|**name**| nvarchar(256) |Nome do grupo de carga de trabalho. Não permite valor nulo.|
|**snapshot_time**| datetime |DateTime do instantâneo de estatísticas do grupo de recursos feito.|
|**duration_ms**| int |Duração entre o instantâneo atual e o anterior.|
|**active_worker_count**| int |Total de trabalhos no instantâneo atual.|
|**active_request_count**| int |Conta de solicitação atual. Não permite valor nulo.|
|**active_session_count**| int |Total de sessões ativas no instantâneo atual.|
|**total_request_count**| bigint |Conta cumulativa de solicitações concluídas no grupo de carga de trabalho. Não permite valor nulo.|
|**delta_request_count**| int |Contagem de solicitações concluídas no grupo de cargas de trabalho desde o último instantâneo. Não permite valor nulo.|
|**total_cpu_usage_ms**| bigint |Uso cumulativo da CPU, em milissegundos, pelo grupo de carga de trabalho. Não permite valor nulo.|
|**delta_cpu_usage_ms**| int |Uso da CPU em milissegundos desde o último instantâneo. Não permite valor nulo.|
|**delta_cpu_usage_preemptive_ms**| int |As chamadas do Win32 preemptivas não são regidas pelo RG da CPU do SQL, desde o último instantâneo.|
|**delta_reads_reduced_memgrant_count**| int |A contagem de concessões de memória que atingiu o limite máximo de tamanho de consulta desde o último instantâneo. Não permite valor nulo.|
|**reads_throttled**| int |Número total de leituras limitadas.|
|**delta_reads_queued**| int |O IOs de leitura total enfileirado desde o último instantâneo. Permite valor nulo. NULL se o grupo de recursos não for regido para e/s.|
|**delta_reads_issued**| int |O IOs de leitura total emitido desde o último instantâneo. Permite valor nulo. NULL se o grupo de recursos não for regido para e/s.|
|**delta_reads_completed**| int |O IOs de leitura total foi concluído desde o último instantâneo. Não permite valor nulo.|
|**delta_read_bytes**| bigint |O número total de bytes lidos desde o último instantâneo. Não permite valor nulo.|
|**delta_read_stall_ms**| int |Tempo total (em milissegundos) entre a chegada de e/s de leitura e a conclusão desde o último instantâneo. Não permite valor nulo.|
|**delta_read_stall_queued_ms**| int |Tempo total (em milissegundos) entre a chegada de e/s de leitura e o problema desde o último instantâneo. Permite valor nulo. NULL se o grupo de recursos não for regido para e/s. Delta_read_stall_queued_ms diferente de zero significa que a e/s está sendo afetada pelo RG.|
|**delta_writes_queued**| int |O IOs de gravação total enfileirado desde o último instantâneo. Permite valor nulo. NULL se o grupo de recursos não for regido para e/s.|
|**delta_writes_issued**| int |O IOs de gravação total emitido desde o último instantâneo. Permite valor nulo. NULL se o grupo de recursos não for regido para e/s.|
|**delta_writes_completed**| int |O IOs de gravação total foi concluído desde o último instantâneo. Não permite valor nulo.|
|**delta_writes_bytes**| bigint |O número total de bytes gravados desde o último instantâneo. Não permite valor nulo.|
|**delta_write_stall_ms**| int |Tempo total (em milissegundos) entre a chegada de e/s de gravação e a conclusão desde o último instantâneo. Não permite valor nulo.|
|**delta_background_writes**| int |O total de gravações realizadas por tarefas em segundo plano desde o último instantâneo.|
|**delta_background_write_bytes**| bigint |O tamanho total de gravação realizado pelas tarefas em segundo plano desde o último instantâneo, em bytes.|
|**delta_log_bytes_used**| bigint |Log usado desde o último instantâneo em bytes.|
|**delta_log_temp_db_bytes_used**| bigint |Log de tempdb usado desde o último instantâneo em bytes.|
|**delta_query_optimizations**| bigint |A contagem de otimizações de consulta neste grupo de carga de trabalho desde o último instantâneo. Não permite valor nulo.|
|**delta_suboptimal_plan_generations**| bigint |A contagem de gerações de planos de qualidade inferior ocorridas neste grupo de cargas de trabalho devido à pressão de memória desde o último instantâneo. Não permite valor nulo.
|**max_memory_grant_kb**| bigint |Concessão máxima de memória para o grupo em KB.|
|**max_request_cpu_msec**| bigint |Uso máximo da CPU, em milissegundos, para uma única solicitação. Não permite valor nulo.|
|**max_concurrent_request**| int |Configuração atual do número máximo de solicitações simultâneas. Não permite valor nulo.|
|**max_io**| int |Limite máximo de e/s para o grupo.|
|**max_global_io**| int |Identificado apenas para fins informativos. Não compatível. A compatibilidade futura não está garantida.
|**max_queued_io**| int |Identificado apenas para fins informativos. Não compatível. A compatibilidade futura não está garantida.|
|**max_log_rate_kb**| bigint |Taxa máxima de log (quilobytes-bytes por segundo) em nível de grupo de recursos.|
|**max_session**| int |Limite de sessão do grupo.|
|**max_worker**| int |Limite de trabalho para o grupo.|
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

## <a name="see-also"></a>Consulte também

- [Governança de taxa de log de tradução](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [Limites de recursos de DTU do pool elástico](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools)
- [Limites de recursos vCore do pool elástico](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools)
