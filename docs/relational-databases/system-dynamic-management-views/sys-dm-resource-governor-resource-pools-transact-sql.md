---
title: sys. dm_resource_governor_resource_pools (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_resource_pools_TSQL
- dm_resource_governor_resource_pools_TSQL
- sys.dm_resource_governor_resource_pools
- dm_resource_governor_resource_pools
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_resource_governor_resource_pools dynamic management view
ms.assetid: 9bfc926e-d8bc-40f8-9229-ab1f8a1e69c5
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ae7fd97640b048d504dd03599bf991e9ae91929d
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827832"
---
# <a name="sysdm_resource_governor_resource_pools-transact-sql"></a>sys.dm_resource_governor_resource_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna informações sobre o estado, a configuração atual e as estatísticas do pool de recursos.  
  
> [!NOTE]  
>  Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use o nome **Sys. dm_pdw_nodes_resource_governor_resource_pools**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|pool_id|**int**|ID do pool de recursos. Não permite valor nulo.|  
|Nome|**sysname**|O nome do pool de recursos. Não permite valor nulo.|  
|statistics_start_time|**datetime**|O momento em que as estatísticas deste pool foram redefinidas. Não permite valor nulo.|  
|total_cpu_usage_ms|**bigint**|O uso cumulativo de CPU em milissegundos desde que as estatísticas do Administrador de Recursos foram redefinidas. Não permite valor nulo.|  
|cache_memory_kb|**bigint**|O uso de memória cache total atual em quilobytes. Não permite valor nulo.|  
|compile_memory_kb|**bigint**|O total atual de uso da memória em quilobytes (KB). Grande parte dessa utilização é para compilação e otimização, mas também pode incluir outros usuários de memória. Não permite valor nulo.|  
|used_memgrant_kb|**bigint**|O total atual de memória usada de concessões de memória. Não permite valor nulo.|  
|total_memgrant_count|**bigint**|A contagem cumulativa de concessões de memória neste pool de recursos. Não permite valor nulo.|  
|total_memgrant_timeout_count|**bigint**|A contagem cumulativa de tempos-limite de concessão de memória nesse pool de recursos. Não permite valor nulo.|  
|active_memgrant_count|**int**|A contagem atual de concessões de memória. Não permite valor nulo.|  
|active_memgrant_kb|**bigint**|A soma, em quilobytes (KB), de concessões de memória atuais. Não permite valor nulo.|  
|memgrant_waiter_count|**int**|A contagem de consultas que estão pendentes em concessões de memória. Não permite valor nulo.|  
|max_memory_kb|**bigint**|A quantidade máxima de memória, em quilobytes, que o pool de recursos pode ter. Tem como base as configurações atuais e o estado do servidor. Não permite valor nulo.|  
|used_memory_kb|**bigint**|A quantidade de memória usada, em quilobytes, para o pool de recursos. Não permite valor nulo.|  
|target_memory_kb|**bigint**|A meta de quantidade de memória, em quilobytes, que o pool de recursos está tentando obter. Tem como base as configurações atuais e o estado do servidor. Não permite valor nulo.|  
|out_of_memory_count|**bigint**|O número de alocações de memória com falha no pool desde que as estatísticas do Administrador de Recursos foram redefinidas. Não permite valor nulo.|  
|min_cpu_percent|**int**|A configuração atual de largura de banda de CPU garantida para todas as solicitações no pool de recursos quando houver contenção de CPU. Não permite valor nulo.|  
|max_cpu_percent|**int**|A configuração atual do máximo de largura de banda de CPU média permitida para todas as solicitações no pool de recursos quando houver contenção de CPU. Não permite valor nulo.|  
|min_memory_percent|**int**|A configuração atual de quantidade de memória garantida para todas as solicitações no pool de recursos quando houver contenção de memória. Não é compartilhada com outros pools de recursos. Não permite valor nulo.|  
|max_memory_percent|**int**|A configuração atual da porcentagem de memória total de servidor que pode ser usada pelas solicitações nesse pool de recursos. Não permite valor nulo.|  
|cap_cpu_percent|**int**|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> Extremidade rígida na largura de banda de CPU que todas as solicitações no pool de recursos receberão. Limita o nível de largura de banda máxima de CPU ao nível especificado. O intervalo permitido para o valor é de 1 a 100. Não permite valor nulo.|  
|min_iops_per_volume|**int**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> A configuração de E/S por segundo (IOPS) mínima por volume de disco deste pool. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S. Ou seja, o pool de recursos MIN_IOPS_PER_VOLUME e as configurações de MAX_IOPS_PER_VOLUME são 0.|  
|max_iops_per_volume|**int**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> A configuração de E/S por segundo (IOPS) máxima por volume de disco deste pool. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S. Ou seja, as configurações do pool de recursos MIN_IOPS_PER_VOLUME e MAX_IOPS_PER_VOLUME são 0.|  
|read_io_queued_total|**int**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> O total de E/S lidas enfileiradas desde que o Administrador de Recursos foi redefinido. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S. Ou seja, o pool de recursos MIN_IOPS_PER_VOLUME e as configurações de MAX_IOPS_PER_VOLUME são 0.|  
|read_io_issued_total|**int**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> O total de E/S lidas emitidas desde que as estatísticas do Administrador de Recursos foram redefinidas. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S. Ou seja, o pool de recursos MIN_IOPS_PER_VOLUME e as configurações de MAX_IOPS_PER_VOLUME são 0.|  
|read_io_completed_total|**int**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> O total de E/S lidas concluídas desde que as estatísticas do Administrador de Recursos foram redefinidas. Não permite valor nulo.|  
|read_io_throttled_total|**int**|O total de E/S lidas limitadas desde que as estatísticas do Administrador de Recursos foram redefinidas. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S. Ou seja, o pool de recursos MIN_IOPS_PER_VOLUME e as configurações de MAX_IOPS_PER_VOLUME são 0.|  
|read_bytes_total|**bigint**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> O número total de bytes lidos desde que as estatísticas do Administrador de Recursos foram redefinidas. Não permite valor nulo.|  
|read_io_stall_total_ms|**bigint**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> Tempo total (em milissegundos) entre a chegada de E/S de leitura e a conclusão. Não permite valor nulo. |  
|read_io_stall_queued_ms|**bigint**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> Tempo total (em milissegundos) entre a chegada de E/S de leitura e a emissão. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S. Ou seja, o pool de recursos MIN_IOPS_PER_VOLUME e as configurações de MAX_IOPS_PER_VOLUME são 0.<br /><br /> Para determinar se a configuração de e/s do pool está causando latência, subtraia **read_io_stall_queued_ms** de **read_io_stall_total_ms**.|  
|write_io_queued_total|**int**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> O total de E/Ss de gravação enfileiradas desde que as estatísticas do Administrador de Recursos foram redefinidas. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S. Ou seja, o pool de recursos MIN_IOPS_PER_VOLUME e as configurações de MAX_IOPS_PER_VOLUME são 0.|  
|write_io_issued_total|**int**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> O total de E/Ss de gravação emitidas desde que as estatísticas do Administrador de Recursos foram redefinidas. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S. Ou seja, o pool de recursos MIN_IOPS_PER_VOLUME e as configurações de MAX_IOPS_PER_VOLUME são 0.|  
|write_io_completed_total|**int**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> O total de E/Ss de gravação concluídas desde que as estatísticas do Administrador de Recursos foram redefinidas. Não permite valor nulo|  
|write_io_throttled_total|**int**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> O total de E/Ss de gravação limitadas desde que as estatísticas do Administrador de Recursos foram redefinidas. Não permite valor nulo|  
|write_bytes_total|**bigint**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> O número total de bytes gravados desde que as estatísticas do Administrador de Recursos foram redefinidas. Não permite valor nulo.|  
|write_io_stall_total_ms|**bigint**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> Tempo total (em milissegundos) entre a chegada de E/S de gravação e a conclusão. Não permite valor nulo. |  
|write_io_stall_queued_ms|**bigint**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> Tempo total (em milissegundos) entre a chegada de E/S de gravação e a emissão. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S. Ou seja, o pool de recursos MIN_IOPS_PER_VOLUME e as configurações de MAX_IOPS_PER_VOLUME são 0.<br /><br /> Este é o atraso introduzido pela administração do recurso de E/S.|  
|io_issue_violations_total|**int**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> Total de violações de problemas de E/S. Ou seja, o número de vezes em que a taxa de problema de E/S era inferior à taxa reservada. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S. Ou seja, o pool de recursos MIN_IOPS_PER_VOLUME e as configurações de MAX_IOPS_PER_VOLUME são 0.|  
|io_issue_delay_total_ms|**bigint**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> Tempo total (em milissegundos) entre o problema agendado e o problema real de E/S. Permite valor nulo. Nulo se o pool de recursos não for administrado para E/S. Ou seja, o pool de recursos MIN_IOPS_PER_VOLUME e as configurações de MAX_IOPS_PER_VOLUME são 0.|  
|pdw_node_id|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="remarks"></a>Comentários  
 Os grupos de cargas de trabalho e os pools de recursos de Administrador de Recursos têm um mapeamento muitos para um. Como resultado, muitas das estatísticas de pool de recursos são extraídas das estatísticas de grupo de carga de trabalho.  
  
 Essa exibição de gerenciamento dinâmico mostra a configuração na memória. Para ver os metadados de configuração armazenados, use a exibição de catálogo sys. resource_governor_resource_pools.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW SERVER STAT.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys. dm_resource_governor_workload_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)   
 [sys. resource_governor_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-resource-pools-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  



