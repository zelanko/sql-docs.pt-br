---
title: sys.dm_resource_governor_resource_pool_volumes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_resource_pool_volumes_TSQL
- dm_resource_governor_resource_pool_volumes_TSQL
- dm_resource_governor_resource_pool_volumes
- sys.dm_resource_governor_resource_pool_volumes
dev_langs:
- TSQL
helpviewer_keywords:
- dm_resource_governor_resource_pool_volumes
- sys.dm_resource_governor_resource_pool_volumes
ms.assetid: fa692e56-c561-4533-97c5-bc12c600553f
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 49c3cc7312978f313ed55147530c371bdde69675
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmresourcegovernorresourcepoolvolumes-transact-sql"></a>sys.dm_resource_governor_resource_pool_volumes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre o pool de recursos atual e estatísticas de e/s para cada volume de disco. Essas informações também estão disponíveis no nível do pool de recursos em [sys.DM resource_governor_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md).  
  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|pool_id|**Int**|ID do pool de recursos. Não permite valor nulo.|  
|volume_name|**sysname**|O nome do volume de disco. Não permite valor nulo.|  
|read_io_queued_total|**Int**|O total / s lidas enfileiradas desde que o administrador de recursos é redefinido. Não permite valor nulo.|  
|read_io_issued_total|**Int**|O total de E/S lidas emitidas desde que as estatísticas do Administrador de Recursos foram redefinidas. Não permite valor nulo.|  
|read_ios_completed_total|**Int**|O total de E/S lidas concluídas desde que as estatísticas do Administrador de Recursos foram redefinidas. Não permite valor nulo.|  
|read_ios_throttled_total|**Int**|O total de E/S lidas limitadas desde que as estatísticas do Administrador de Recursos foram redefinidas. Não permite valor nulo.|  
|read_bytes_total|**bigint**|O número total de bytes lidos desde que as estatísticas do Administrador de Recursos foram redefinidas. Não permite valor nulo.|  
|read_io_stall_total_ms|**bigint**|Tempo total (em milissegundos) entre a chegada de E/S de leitura e a conclusão. Não permite valor nulo.|  
|read_io_stall_queued_ms|**bigint**|Tempo total (em milissegundos) entre a chegada de E/S de leitura e a emissão. Este é o atraso introduzido pela administração do recurso de E/S. Não permite valor nulo.|  
|write_io_queued_total|**Int**|O total de E/Ss de gravação enfileiradas desde que as estatísticas do Administrador de Recursos foram redefinidas. Não permite valor nulo.|  
|write_io_issued_total|**Int**|O total de E/Ss de gravação emitidas desde que as estatísticas do Administrador de Recursos foram redefinidas. Não permite valor nulo.|  
|write_io_completed_total|**Int**|O total de E/Ss de gravação concluídas desde que as estatísticas do Administrador de Recursos foram redefinidas. Não permite valor nulo|  
|write_io_throttled_total|**Int**|O total de E/Ss de gravação limitadas desde que as estatísticas do Administrador de Recursos foram redefinidas. Não permite valor nulo|  
|write_bytes_total|**bigint**|O número total de bytes gravados desde que as estatísticas do Administrador de Recursos foram redefinidas. Não permite valor nulo.|  
|write_io_stall_total_ms|**bigint**|Tempo total (em milissegundos) entre o problema de E/S de gravação e a conclusão. Não permite valor nulo.|  
|write_io_stall_queued_ms|**bigint**|Tempo total (em milissegundos) entre a chegada de E/S de gravação e a emissão. Este é o atraso introduzido pela administração do recurso de E/S. Não permite valor nulo.|  
|io_issue_violations_total|**Int**|Total de violações de problemas de E/S. Ou seja, o número de vezes em que a taxa de problema de E/S era inferior à taxa reservada. Não permite valor nulo.|  
|io_issue_delay_total_ms|**bigint**|Tempo total (em milissegundos) entre o problema agendado e o problema real de E/S. Não permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW SERVER STAT.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys.dm_resource_governor_workload_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)   
 [sys.resource_governor_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-resource-pools-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  

