---
title: sys.dm_exec_dms_workers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
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
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8a31b03208eba573fc6bd50f2348733ef0a07c2b
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52418357"
---
# <a name="sysdmexecdmsworkers-transact-sql"></a>sys.dm_exec_dms_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contém informações sobre todos os trabalhadores concluindo as etapas do DMS.  
  
 Essa exibição mostra os dados para os últimos 1000 solicitações e solicitações ativas; solicitações ativas sempre têm os dados presentes nesta exibição.  
  
|Nome da coluna|Tipo de Dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|Consulta que este trabalhador DMS é parte of.request_id, step_index, e dms_step_index formam a chave para esta exibição.||  
|step_index|**int**|Etapa que este trabalhador DMS faz parte de consulta.|Veja o índice da etapa na [DM exec_distributed_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md).|  
|dms_step_index|**int**|Etapa no plano de DMS que este trabalhador está executando.|Consulte [sys.dm_exec_dms_workers (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)|  
|compute_node_id|**int**|Nó que o trabalhador está sendo executado.|Ver [DM exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|distribution_id|**int**|||  
|Tipo|**nvarcha(32)**|||  
|status|**nvarchar(32)**|Status desta etapa|'Pendente', 'Running', 'Completa', 'Falha', 'UndoFailed', 'PendingCancel', 'Cancelar', 'Desfeita', 'Anulada'|  
|bytes_per_sec|**bigint**|||  
|bytes_processed|**bigint**|||  
|rows_processed|**bigint**|||  
|start_time|**datetime**|Hora em que a etapa começou execução|Menor ou igual à hora atual e maior ou igual a end_compile_time da consulta ao qual pertence essa etapa.|  
|end_time|**datetime**|Hora em que esta etapa concluiu a execução, foi cancelada ou falhou.|Menor ou igual à hora atual e maior ou igual a start_time, definido como NULL para etapas atualmente em execução ou na fila.|  
|total_elapsed_time|**int**|Quantidade total de tempo de que execução a etapa de consulta, em milissegundos|Entre 0 e a diferença entre end_time e start_time. 0 para etapas em fila.|  
|cpu_time|**bigint**|||  
|query_time|**int**|||  
|buffers_available|**int**|||  
|dms_cpid|**int**|||  
|sql_spid|**int**|||  
|error_id|**nvarchar(36)**|||  
|source_info|**nvarchar(4000)**|||  
|destination_info|**nvarchar(4000)**|||  
|command|**nvarchar(4000)**|||  
  
## <a name="see-also"></a>Consulte também  
 [Solução de problemas com exibições de gerenciamento dinâmico do PolyBase](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Banco de dados relacionados a exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
