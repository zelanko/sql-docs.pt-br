---
description: sys.dm_resource_governor_resource_pools_history_ex (Transact-SQL)
title: sys.dm_resource_governor_resource_pools_history_ex (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.resource_governor
- sys.resource_governor_TSQL
- resource_governor
- resource_governor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governor catalog view
ms.assetid: ''
author: joesackmsft
ms.author: josack
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: 1cbc5d23a7c7843a2186cd951fd5bb16079489d3
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/08/2020
ms.locfileid: "91834325"
---
# <a name="sysdm_resource_governor_resource_pools_history_ex-transact-sql"></a>sys.dm_resource_governor_resource_pools_history_ex (Transact-SQL)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

Retorna o instantâneo em um intervalo de 20 segundos para os últimos 32 minutos (128 Recs no total) de estatísticas de pools de recursos para um banco de dados SQL do Azure.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**pool_id**|INT|ID do pool de recursos. Não permite valor nulo.
|**name**|sysname|O nome do pool de recursos. Não permite valor nulo.|
|**snapshot_time**|datetime2|DateTime do instantâneo de estatísticas do pool de recursos tirado|
|**duration_ms**|INT|Duração entre o instantâneo atual e o anterior|
|**statistics_start_time**|datetime2|O momento em que as estatísticas deste pool foram redefinidas. Não permite valor nulo.|
|**active_session_count**|INT|Total de sessões ativas no instantâneo atual|
|**active_worker_count**|INT|Total de trabalhos no instantâneo atual|
|**delta_cpu_usage_ms**|INT|Uso da CPU em milissegundos desde o último instantâneo. Não permite valor nulo.|
|**delta_cpu_usage_preemptive_ms**|INT|Chamadas do Win32 preemptivas não governadas pelo RG da CPU do SQL, desde o último instantâneo|
|**used_data_space_kb**|BIGINT|Espaço total usado nos bancos de dados de usuário associados ao pool de usuários|
|**allocated_disk_space_kb**|BIGINT|Tamanho total do arquivo de dados do usuário no pool associado ao usuário|
|**target_memory_kb**|BIGINT|A meta de quantidade de memória, em quilobytes, que o pool de recursos está tentando obter. Tem como base as configurações atuais e o estado do servidor. Não permite valor nulo.|
|**used_memory_kb**|BIGINT|A quantidade de memória usada, em quilobytes, para o pool de recursos. Não permite valor nulo.|
|**cache_memory_kb**|BIGINT|O uso de memória cache total atual em quilobytes. Não permite valor nulo.|
|**compile_memory_kb**|BIGINT|O total atual de uso da memória em quilobytes (KB). Grande parte dessa utilização é para compilação e otimização, mas também pode incluir outros usuários de memória. Não permite valor nulo.|
|**active_memgrant_count**|BIGINT|A contagem atual de concessões de memória. Não permite valor nulo.|
|**active_memgrant_kb**|BIGINT|A soma, em quilobytes (KB), de concessões de memória atuais. Não permite valor nulo.|
|**used_memgrant_kb**|BIGINT|O total atual de memória usada de concessões de memória. Não permite valor nulo.|
|**delta_memgrant_timeout_count**|INT|contagem de tempos limite de concessão de memória neste pool de recursos neste período. Não permite valor nulo.|
|**delta_memgrant_waiter_count**|INT|A contagem de consultas que estão pendentes em concessões de memória. Não permite valor nulo.|
|**delta_out_of_memory_count**|INT|O número de alocações de memória com falha no pool desde o último instantâneo. Não permite valor nulo.|
|**delta_read_io_queued**|INT|O IOs de leitura total enfileirado desde o último instantâneo. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S.|
|**delta_read_io_issued**|INT|O IOs de leitura total emitido desde o último instantâneo. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S.|
|**delta_read_io_completed**|INT|O IOs de leitura total foi concluído desde o último instantâneo. Não permite valor nulo.|
|**delta_read_io_throttled**|INT|O total de leitura do IOs foi limitado desde o instantâneo. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S.|
|**delta_read_bytes**|BIGINT|O número total de bytes lidos desde o último instantâneo. Não permite valor nulo.|
|**delta_read_io_stall_ms**|INT|Tempo total (em milissegundos) entre a chegada de e/s de leitura e a conclusão desde o último instantâneo. Não permite valor nulo.|
|**delta_read_io_stall_queued_ms**|INT|Tempo total (em milissegundos) entre a chegada de e/s de leitura e o problema desde o último instantâneo. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S. Delta_read_io_stall_queued_ms diferente de zero significa que a e/s está sendo afetada pelo RG.|
|**delta_write_io_queued**|INT|O IOs de gravação total enfileirado desde o último instantâneo. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S.|
|**delta_write_io_issued**|INT|O IOs de gravação total emitido desde o último instantâneo. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S.|
|**delta_write_io_completed**|INT|O IOs de gravação total foi concluído desde o último instantâneo. Não permite valor nulo|
|**delta_write_io_throttled**|INT|O total de gravação do IOs foi limitado desde o último instantâneo. Não permite valor nulo|
|**delta_write_bytes**|BIGINT|O número total de bytes gravados desde o último instantâneo. Não permite valor nulo.|
|**delta_write_io_stall_ms**|INT|Tempo total (em milissegundos) entre a chegada de e/s de gravação e a conclusão desde o último instantâneo. Não permite valor nulo.|
|**delta_write_io_stall_queued_ms**|INT|Tempo total (em milissegundos) entre a chegada de e/s de gravação e o problema desde o último instantâneo. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S.|
|**delta_io_issue_delay_ms**|INT|Tempo total (em milissegundos) entre o problema agendado e o problema real da e/s desde o último instantâneo. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S.|
|**max_iops_per_volume**|INT|A configuração de volume de e/s (IOPS) máxima por segundo do disco para este pool. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S.|
|**max_memory_kb**|BIGINT|A quantidade máxima de memória, em quilobytes, que o pool de recursos pode ter. Tem como base as configurações atuais e o estado do servidor. Não permite valor nulo.
|**max_log_rate_kb**|BIGINT|Taxa máxima de log (quilobytes-bytes por segundo) no nível do pool de recursos.|
|**max_data_space_kb**|BIGINT|Configuração máxima do limite de armazenamento do pool elástico para esse pool elástico em kilobytes.|
|**max_session**|INT|Limite de sessão para o pool|
|**max_worker**|INT|Limite de trabalho para o pool|
|**min_cpu_percent**|INT|A configuração atual de largura de banda de CPU garantida para todas as solicitações no pool de recursos quando houver contenção de CPU. Não permite valor nulo.|
|**max_cpu_percent**|INT|A configuração atual do máximo de largura de banda de CPU média permitida para todas as solicitações no pool de recursos quando houver contenção de CPU. Não permite valor nulo.|
|**cap_cpu_percent**|INT|Extremidade rígida na largura de banda de CPU que todas as solicitações no pool de recursos receberão. Limita o nível de largura de banda máxima de CPU ao nível especificado. O intervalo permitido para o valor é de 1 a 100. Não permite valor nulo.|
|**min_vcores**|decimal (5, 2)|A configuração atual de largura de banda de CPU garantida para todas as solicitações no pool de recursos quando houver contenção de CPU.  Em unidades de vCores|
|**max_vcores**|decimal (5, 2)|A configuração atual do máximo de largura de banda de CPU média permitida para todas as solicitações no pool de recursos quando houver contenção de CPU.  Na unidade de vCores|
|**cap_vcores**|decimal (5, 2)|Extremidade rígida na largura de banda de CPU que todas as solicitações no pool de recursos receberão.  Na unidade em vCores|
|**instance_cpu_count**|INT|Número de CPU configurada para a instância|
|**instance_cpu_percent**|decimal (5, 2)|Porcentagem de CPU configurada para a instância|
|**instance_vcores**|decimal (5, 2)|Número de vCores configuradas para a instância|
|**delta_log_bytes_used**|decimal (5, 2)|Geração de log total (em bytes) no nível do pool desde o último instantâneo|
|**avg_login_rate_percent**|decimal (5, 2)|Número de logons desde o último instantâneo, em comparação com o limite de logon|
|**delta_vcores_used**|decimal (5, 2)|Utilização de computação na contagem de vCores desde o último instantâneo.|
|**cap_vcores_used_percent**|decimal (5, 2)|Média de utilização da computação em percentual do limite do pool.|
|**instance_vcores_used_percent**|decimal (5, 2)|Média de utilização de computação em porcentagem do limite da instância do SQL.|
|**avg_data_io_percent**|decimal (5, 2)|Média de utilização de E/S em percentual do limite do pool.|
|**avg_log_write_percent**|decimal (5, 2)|Média de utilização dos recursos de gravação em percentual do limite do pool.|
|**avg_storage_percent**|decimal (5, 2)|Média de utilização do armazenamento em percentual do limite de armazenamento do pool.|
|**avg_allocated_storage_percent**|decimal (5, 2)|A porcentagem de espaço de dados alocada por todos os bancos de dado no pool elástico. Esta é a taxa de espaço de dados alocada para o tamanho máximo de dados para o pool elástico. Para obter mais informações, consulte: gerenciamento de espaço de arquivo no banco de dados SQL|
|**max_worker_percent**|decimal (5, 2)|Máximo de trabalhos (solicitações) simultâneos em percentual, com base no limite do pool.|
|**max_session_percent**|decimal (5, 2)|Número máximo de sessões simultâneas em percentual, com base no limite do pool.|
|||

## <a name="permissions"></a>Permissões

Esta exibição requer a permissão VIEW SERVER STATE.

## <a name="remarks"></a>Comentários

Os usuários podem acessar essa exibição de gerenciamento dinâmico para monitorar o consumo de recursos quase em tempo real para o pool de carga de trabalho do usuário, bem como os pools internos do sistema da instância do banco de dados SQL

> [!IMPORTANT]
> A maioria dos dados exibidos por essa DMV destina-se ao consumo interno e está sujeita a alterações.

## <a name="examples"></a>Exemplos

O exemplo a seguir retorna dados de taxa de log máximos e consumo em cada instantâneo pelo pool de usuários  

```sql
select snapshot_time, name, max_log_rate_kb, delta_log_bytes_used from sys.dm_resource_governor_resource_pools_history_ex where name like 'UserPool%' order by snapshot_time desc
```

O exemplo a seguir retorna informações semelhantes como sys.elastic_pool_resource_stats sem precisar se conectar ao mestre lógico

```sql
select snapshot_time, name, cap_vcores_used_percent,
  avg_data_io_percent,  
  avg_log_write_percent,
  avg_storage_percent,
  avg_allocated_storage_percent,
  max_data_space_kb,
  max_worker_percent,
  max_session_percent
    from sys.dm_resource_governor_resource_pools_history_ex where name like 'UserPool%' order by snapshot_time desc
```

## <a name="see-also"></a>Consulte Também

- [Governança de taxa de log de tradução](/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [Limites de recursos DTU do pool elástico](/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools)
- [Limites de recursos vCore do pool elástico](/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools)