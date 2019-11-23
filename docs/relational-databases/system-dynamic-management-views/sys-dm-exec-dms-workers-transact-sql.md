---
title: sys.dm_exec_dms_workers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.DM_EXEC_DMS_WORKERS_TSQL
- DM_EXEC_DMS_WORKERS_TSQL
- DM_EXEC_DMS_WORKERS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_dms_workers management view
- sys.dm_exec_dms_workers management view
ms.assetid: f468da29-78c3-4f10-8a3c-17905bbf46f2
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6fd005563251ba674449020c7af25ce20ea98b4a
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532938"
---
# <a name="sysdm_exec_dms_workers-transact-sql"></a>sys.dm_exec_dms_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contém informações sobre todos os trabalhos concluindo as etapas de DMS.  
  
 Esta exibição mostra os dados das últimas 1000 solicitações e solicitações ativas; as solicitações ativas sempre têm os dados presentes nessa exibição.  
  
|Column Name|Tipo de dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|`nvarchar(32)`|Consulte se esse trabalho DMS faz parte de. request_id, step_index e dms_step_index formam a chave para essa exibição.||  
|step_index|`int`|Etapa de consulta para a qual este trabalho DMS faz parte.|Consulte índice de etapa em [Sys. &#40;DM_EXEC_DISTRIBUTED_REQUEST_STEPS Transact-&#41;SQL](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md).|  
|dms_step_index|`int`|Etapa no plano DMS que esse trabalho está executando.|Consulte [Sys. dm_exec_dms_workers (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)|  
|compute_node_id|`int`|Nó no qual o trabalho está sendo executado.|Consulte [Sys. dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|distribution_id|`int`|||  
|Tipo|`nvarcha(32)`|||  
|status|`nvarchar(32)`|Status desta etapa|'Pending', 'Running', 'Complete', 'Failed', 'UndoFailed', 'PendingCancel', 'Cancelled', 'Undone', 'Aborted'|  
|bytes_per_sec|`bigint`|||  
|bytes_processed|`bigint`|||  
|rows_processed|`bigint`|||  
|start_time|`datetime`|Hora em que a execução da etapa foi iniciada|Menor ou igual à hora atual e maior ou igual a end_compile_time da consulta à qual essa etapa pertence.|  
|end_time|`datetime`|A hora em que esta etapa concluiu a execução, foi cancelada ou falhou.|Menor ou igual à hora atual e maior ou igual a start_time, definido como nulo para as etapas atualmente em execução ou na fila.|  
|total_elapsed_time|`int`|Quantidade total de tempo que a etapa de consulta foi executada, em milissegundos|Entre 0 e a diferença entre end_time e start_time. 0 para etapas em fila.|  
|cpu_time|`bigint`|||  
|query_time|`int`|||  
|buffers_available|`int`|||  
|dms_cpid|`int`|||  
|sql_spid|`int`|||  
|error_id|`nvarchar(36)`|||  
|source_info|`nvarchar(4000)`|||  
|destination_info|`nvarchar(4000)`|||  
|command|`nvarchar(4000)`|||
|compute_pool_id|`int`|Identificador exclusivo do pool.|

## <a name="see-also"></a>Consulte também  
 [Solução de problemas do polybase com exibições de gerenciamento dinâmico](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições &#40;de gerenciamento dinâmico relacionadas ao banco de dados TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
