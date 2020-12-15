---
description: sys.dm_resource_governor_external_resource_pools (Transact-SQL)
title: sys.dm_resource_governor_external_resource_pools (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.technology: machine-learning-services
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_external_resource_pools_TSQL
- sys.dm_resource_governor_external_resource_pools
- dm_resource_governor_external_resource_pools
- dm_resource_governor_external_resource_pools_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_resource_governor_external_resource_pools
- sys.dm_resource_governor_external_resource_pools
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: 1fdce8416bf28b1013b32efb5c2d1dc46c76831d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484588"
---
# <a name="sysdm_resource_governor_external_resource_pools-transact-sql"></a>sys.dm_resource_governor_external_resource_pools (Transact-SQL)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Retorna informações sobre o estado atual do pool de recursos externos, a configuração atual dos pools de recursos e as estatísticas do pool de recursos. 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
|Nome da coluna      |Tipo de dados      |Descrição|  
|----------------|---------------|-----------------| 
| external_pool_id|**int**|ID do pool de recursos. Não permite valor nulo. |
| name|**sysname**|O nome do pool de recursos. Não permite valor nulo. 
| pool_version|**int**|Número de versão interno.|
| max_cpu_percent|**int**|A configuração atual do máximo de largura de banda de CPU média permitida para todas as solicitações no pool de recursos quando houver contenção de CPU. Não permite valor nulo. |
| max_processes|**int**|Número máximo de processos externos simultâneos. O valor padrão, 0, não especifica nenhum limite. Não permite valor nulo.|
| max_memory_percent|**int**|A configuração atual da porcentagem de memória total de servidor que pode ser usada pelas solicitações nesse pool de recursos. Não permite valor nulo. |
| statistics_start_time|**datetime**|O momento em que as estatísticas deste pool foram redefinidas. Não permite valor nulo. 
| peak_memory_kb|**bigint**|A quantidade máxima de memória usada, em quilobytes, para o pool de recursos. Não permite valor nulo. |
| write_io_count|**int**|O total de E/Ss de gravação emitidas desde que as estatísticas do Resource Governor foram redefinidas. Não permite valor nulo. |
| read_io_count|**int**|O total de E/S lidas emitidas desde que as estatísticas do Resource Governor foram redefinidas. Não permite valor nulo. |
| total_cpu_kernel_ms|**bigint**|O tempo do kernel do usuário da CPU cumulativo em milissegundos desde que as estatísticas do Resource Governor foram redefinidas. Não permite valor nulo. |
| total_cpu_user_ms|**bigint**|O tempo de do usuário da CPU cumulativo em milissegundos desde que as estatísticas do Resource Governor foram redefinidas. Não permite valor nulo. |
| active_processes_count|**int**|O número de processos externos em execução no momento da solicitação. Não permite valor nulo. |

 
## <a name="permissions"></a>Permissões

Requer a permissão `VIEW SERVER STATE`.

## <a name="see-also"></a>Consulte Também  
 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
