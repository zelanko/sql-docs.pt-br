---
title: sys.dm_resource_governor_resource_pools_history_ex (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: ''
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
manager: craigg
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: d585f1f1245457aa9051f25bca696cf4495d93ed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66743921"
---
# <a name="sysdmresourcegovernorresourcepoolshistoryex-transact-sql"></a>sys.dm_resource_governor_resource_pools_history_ex (Transact-SQL)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

Os pools de instantâneo retorna no intervalo de 15 segundos para os últimos 30 minutos do recurso de estatísticas para um banco de dados do SQL Azure.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**pool_id**|INT|ID do pool de recursos. Não permite valor nulo.
|**name**|sysname|O nome do pool de recursos. Não permite valor nulo.|
|**snapshot_time**|datetime2|Data e hora do instantâneo resource pool stats tirado|
|**duration_ms**|INT|Duração entre o instantâneo atual e anterior|
|**statistics_start_time**|datetime2|O momento em que as estatísticas deste pool foram redefinidas. Não permite valor nulo.|
|**active_session_count**|INT|Total de sessões Active Directory no instantâneo atual|
|**active_worker_count**|INT|Total de funcionários no instantâneo atual|
|**delta_cpu_usage_ms**|INT|Uso da CPU em milissegundos desde o último instantâneo. Não permite valor nulo.|
|**delta_cpu_usage_preemptive_ms**|INT|Controlam chamadas win32 PreEmptive por RG de CPU do SQL, desde o último instantâneo|
|**used_data_space_kb**|BIGINT|Espaço total usado em bancos de dados de usuário associados ao pool de usuário|
|**allocated_disk_space_kb**|BIGINT|Total de dados tamanho dos bancos de dados de usuário do arquivo associado ao pool de usuário|
|**target_memory_kb**|BIGINT|A meta de quantidade de memória, em quilobytes, que o pool de recursos está tentando obter. Tem como base as configurações atuais e o estado do servidor. Não permite valor nulo.|
|**used_memory_kb**|BIGINT|A quantidade de memória usada, em quilobytes, para o pool de recursos. Não permite valor nulo.|
|**cache_memory_kb**|BIGINT|O uso de memória cache total atual em quilobytes. Não permite valor nulo.|
|**compile_memory_kb**|BIGINT|O total atual de uso da memória em quilobytes (KB). Grande parte dessa utilização é para compilação e otimização, mas também pode incluir outros usuários de memória. Não permite valor nulo.|
|**active_memgrant_count**|BIGINT|A contagem atual de concessões de memória. Não permite valor nulo.|
|**active_memgrant_kb**|BIGINT|A soma, em quilobytes (KB), de concessões de memória atuais. Não permite valor nulo.|
|**used_memgrant_kb**|BIGINT|O total atual de memória usada de concessões de memória. Não permite valor nulo.|
|**delta_memgrant_timeout_count**|INT|Contagem de memória conceder tempos limite nesse pool de recursos nesse período. Não permite valor nulo.|
|**delta_memgrant_waiter_count**|INT|A contagem de consultas que estão pendentes em concessões de memória. Não permite valor nulo.|
|**delta_out_of_memory_count**|INT|O número de alocações de memória com falha no pool desde o último instantâneo. Não permite valor nulo.|
|**delta_read_io_queued**|INT|O total de leitura lidas enfileiradas desde o último instantâneo. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S.|
|**delta_read_io_issued**|INT|O total lidas emitidas desde o último instantâneo. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S.|
|**delta_read_io_completed**|INT|O total lidas concluídas desde o último instantâneo. Não permite valor nulo.|
|**delta_read_io_throttled**|INT|O total lidas limitadas desde o último instantâneo. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S.|
|**delta_read_bytes**|BIGINT|O número total de bytes lidos desde o último instantâneo. Não permite valor nulo.|
|**delta_read_io_stall_ms**|INT|Tempo total (em milissegundos) entre a chegada de e/s de leitura e a conclusão desde o último instantâneo. Não permite valor nulo.|
|**delta_read_io_stall_queued_ms**|INT|Tempo total (em milissegundos) entre a chegada de e/s de leitura e problema desde o último instantâneo. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S. Delta_read_io_stall_queued_ms diferente de zero significa que a e/s está sendo afetado pelo RG.|
|**delta_write_io_queued**|INT|O total SS de gravação enfileiradas desde o último instantâneo. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S.|
|**delta_write_io_issued**|INT|O total de gravação emitidas desde o último instantâneo de IOs. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S.|
|**delta_write_io_completed**|INT|O total de gravação concluídas desde o último instantâneo de IOs. Não permite valor nulo|
|**delta_write_io_throttled**|INT|O total de gravação limitadas do IOs desde o último instantâneo. Não permite valor nulo|
|**delta_write_bytes**|BIGINT|O número total de bytes gravados desde o último instantâneo. Não permite valor nulo.|
|**delta_write_io_stall_ms**|INT|Tempo total (em milissegundos) entre a chegada de e/s de gravação e conclusão desde o último instantâneo. Não permite valor nulo.|
|**delta_write_io_stall_queued_ms**|INT|Tempo total (em milissegundos) entre a chegada de e/s de gravação e problema desde o último instantâneo. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S.|
|**delta_io_issue_delay_ms**|INT|Tempo total (em milissegundos) entre o problema agendado e o problema real de e/s desde o último instantâneo. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S.|
|**max_iops_per_volume**|INT|O máximo e/s por segundo (IOPS) por configuração de volume de disco deste pool. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S.|
|**max_memory_kb**|BIGINT|A quantidade máxima de memória, em quilobytes, que o pool de recursos pode ter. Tem como base as configurações atuais e o estado do servidor. Não permite valor nulo.
|**max_log_rate_kb**|BIGINT|Taxa de log máximo (-quilobytes por segundo) no nível do pool de recursos.|
|**max_data_space_kb**|BIGINT|Limite de armazenamento máximo do pool Elástico definindo para este pool Elástico em quilobytes.|
|**max_session**|INT|Limite de sessão para o pool|
|**max_worker**|INT|Limite de trabalho para o pool|
|**min_cpu_percent**|INT|A configuração atual de largura de banda de CPU garantida para todas as solicitações no pool de recursos quando houver contenção de CPU. Não permite valor nulo.|
|**max_cpu_percent**|INT|A configuração atual do máximo de largura de banda de CPU média permitida para todas as solicitações no pool de recursos quando houver contenção de CPU. Não permite valor nulo.|
|**cap_cpu_percent**|INT|Extremidade rígida na largura de banda de CPU que todas as solicitações no pool de recursos receberão. Limita o nível de largura de banda máxima de CPU ao nível especificado. O intervalo permitido para o valor é de 1 a 100. Não permite valor nulo.|
|**min_vcores**|decimal(5,2)|A configuração atual de largura de banda de CPU garantida para todas as solicitações no pool de recursos quando houver contenção de CPU.  Em unidades de vCores|
|**max_vcores**|decimal(5,2)|A configuração atual do máximo de largura de banda de CPU média permitida para todas as solicitações no pool de recursos quando houver contenção de CPU.  Na unidade de vCores|
|**cap_vcores**|decimal(5,2)|Extremidade rígida na largura de banda de CPU que todas as solicitações no pool de recursos receberão.  Na unidade de vCores|
|**instance_cpu_count**|INT|Número de CPU configurada para a instância|
|**instance_cpu_percent|decimal(5,2)|Porcentagem de CPU configuradas para a instância|
|**instance_vcores**|decimal(5,2)|Número de vCores configuradas para a instância|
|**delta_log_bytes_used**|decimal(5,2)|Geração de log total (em bytes) no nível do pool desde o último instantâneo|
|**avg_login_rate_percent**|decimal(5,2)|Número de logons desde o último instantâneo, comparado em relação ao limite de logon|
|**delta_vcores_used**|decimal(5,2)|A utilização de computação na contagem de vCores desde o último instantâneo.|
|**cap_vcores_used_percent**|decimal(5,2)|Média de utilização em porcentagem do limite do pool de computação.|
|**instance_vcores_used_percent**|decimal(5,2)|Média de utilização da computação em percentual do limite da instância do SQL.|
|**avg_data_io_percent**|decimal(5,2)|Utilização média de e/s em percentagem com base no limite do pool.|
|**avg_log_write_percent**|decimal(5,2)|Média de utilização de recursos de gravação em percentual do limite do pool.|
|**avg_storage_percent**|decimal(5,2)|Média de utilização de armazenamento em percentual do limite do pool de armazenamento.|
|**avg_allocated_storage_percent**|decimal(5,2)|A porcentagem de espaço de dados alocado por todos os bancos de dados no pool Elástico. Esta é a razão do espaço de dados alocado para o tamanho máximo dos dados para o pool Elástico. Para obter mais informações, consulte: Gerenciamento de espaço de arquivo no banco de dados SQL|
|**max_worker_percent**|decimal(5,2)|Máximo de trabalhos simultâneos (solicitações) em porcentagem do limite do pool.|
|**max_session_percent**|decimal(5,2)|Máximo de sessões simultâneas em percentual, com base no limite do pool.|
|||

## <a name="permissions"></a>Permissões

Este modo de exibição requer a permissão VIEW SERVER STATE.

## <a name="remarks"></a>Comentários

Os usuários podem acessar este modo de exibição de gerenciamento dinâmico para monitorar quase em tempo real de consumo de recursos para o pool de carga de trabalho do usuário, bem como os pools do sistema interno da instância de banco de dados SQL.

> [!IMPORTANT]
> A maioria dos dados apresentados por esta DMV destina-se para consumo interno e está sujeita a alterações.

## <a name="examples"></a>Exemplos

O exemplo a seguir retorna dados de taxa de log máximo e consumo de cada instantâneo por pool de usuário  

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

## <a name="see-also"></a>Consulte também

- [Governança de taxa de log de conversão](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [Limites de recursos DTU do pool Elástico](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools)
- [Limites de recursos do pool Elástico vCore](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools)
