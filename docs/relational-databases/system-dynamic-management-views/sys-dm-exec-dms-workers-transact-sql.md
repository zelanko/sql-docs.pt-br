---
title: sys.dm_exec_dms_workers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 940857ee9b723eed5adf1626d8db8c7868d30e7c
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34464742"
---
# <a name="sysdmexecdmsworkers-transact-sql"></a>sys.dm_exec_dms_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contém informações sobre todos os trabalhadores etapas DMS.  
  
 Essa exibição mostra os dados para o último 1000 solicitações e solicitações ativas; solicitações ativas sempre têm os dados presentes nesta exibição.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|Se este trabalhador DMS é parte of.request_id, step_index, e dms_step_index formam a chave para este modo de exibição de consulta.||  
|step_index|**Int**|Etapa que este trabalhador DMS faz parte de consulta.|Consulte o índice de etapa na [sys.dm_exec_distributed_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md).|  
|dms_step_index|**Int**|Etapa no plano de DMS que este trabalhador está em execução.|Consulte [sys.dm_exec_dms_workers (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)|  
|compute_node_id|**Int**|Nó que o trabalho está em execução no.|Consulte [sys.DM exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|distribution_id|**Int**|||  
|Tipo|**nvarcha(32)**|||  
|status|**nvarchar(32)**|Status desta etapa|'Pendente', 'Executar', 'Completa', 'Com falha', 'UndoFailed', 'PendingCancel', 'cancelado', 'Desfeita', 'Anulada'|  
|bytes_per_sec|**bigint**|||  
|bytes_processed|**bigint**|||  
|rows_processed|**bigint**|||  
|start_time|**datetime**|Hora em que a etapa iniciou a execução|Menor ou igual à hora atual e maior ou igual a end_compile_time da consulta ao qual pertence essa etapa.|  
|end_time|**datetime**|Hora em que esta etapa concluiu a execução, foi cancelada ou falha.|Menor ou igual à hora atual e maior ou igual a start_time, definida como NULL para etapas atualmente em execução ou na fila.|  
|total_elapsed_time|**Int**|Quantidade total de tempo de que execução de etapa de consulta, em milissegundos|Entre 0 e a diferença entre start_time e end_time. 0 para etapas em fila.|  
|cpu_time|**bigint**|||  
|query_time|**Int**|||  
|buffers_available|**Int**|||  
|dms_cpid|**Int**|||  
|sql_spid|**Int**|||  
|error_id|**nvarchar(36)**|||  
|source_info|**nvarchar(4000)**|||  
|destination_info|**nvarchar(4000)**|||  
|command|**nvarchar(4000)**|||  
  
## <a name="see-also"></a>Consulte também  
 [PolyBase, solucionando problemas com exibições de gerenciamento dinâmico](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Banco de dados relacionados a exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
