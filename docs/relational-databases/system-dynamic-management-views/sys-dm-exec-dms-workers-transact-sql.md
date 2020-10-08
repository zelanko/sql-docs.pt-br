---
description: sys.dm_exec_dms_workers (Transact-SQL)
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5942abbdd1710a058ec725e88d96f99c9ba21e37
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/08/2020
ms.locfileid: "91834093"
---
# <a name="sysdm_exec_dms_workers-transact-sql"></a>sys.dm_exec_dms_workers (Transact-SQL)
[!INCLUDE [sqlserver2016-asa-pdw](../../includes/applies-to-version/sqlserver2016-asa-pdw.md)]

  Contém informações sobre todos os trabalhos concluindo as etapas de DMS.  
  
 Esta exibição mostra os dados das últimas 1000 solicitações e solicitações ativas; as solicitações ativas sempre têm os dados presentes nessa exibição.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|`nvarchar(32)`|Consulta de que esse trabalho DMS faz parte. <br /><br /> execution_id, step_index e dms_step_index formam a chave para essa exibição.||  
|step_index|`int`|Etapa de consulta para a qual este trabalho DMS faz parte.|Consulte o índice de etapa em [sys.dm_exec_distributed_request_steps &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md).|  
|dms_step_index|`int`|Etapa no plano DMS que esse trabalho está executando.|Consulte [Sys.dm_exec_dms_workers (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)|  
|compute_node_id|`int`|Nó no qual o trabalho está sendo executado.|Confira [sys.dm_exec_compute_nodes &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|distribution_id|`int`|||  
|type|`nvarchar(32)`|Tipo de thread de trabalho do DMS que essa entrada representa.|' DIRECT_CONVERTER ', ' DIRECT_READER ', ' FILE_READER ', ' HASH_CONVERTER ', ' HASH_READER ', ' ROUNDROBIN_CONVERTER ', ' EXPORT_READER ', ' EXTERNAL_READER ', ' EXTERNAL_WRITER ', ' PARALLEL_COPY_READER ', ' REJECT_WRITER ', ' GRAVADOR '|  
|status|`nvarchar(32)`|Status desta etapa|' Pendente ', ' em execução ', ' Concluído ', ' falha ', ' UndoFailed ', ' PendingCancel ', ' cancelado ', ' desfeito ', ' anulado '|  
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
|.|`nvarchar(4000)`|||
|compute_pool_id|`int`|Identificador exclusivo do pool.|

## <a name="see-also"></a>Consulte Também  
 [Solução de problemas do polybase com exibições de gerenciamento dinâmico](/previous-versions/sql/sql-server-2016/mt146389(v=sql.130))   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas ao banco de dados &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
