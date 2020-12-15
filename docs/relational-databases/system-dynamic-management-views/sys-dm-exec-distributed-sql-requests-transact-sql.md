---
description: sys.dm_exec_distributed_sql_requests (Transact-SQL)
title: sys.dm_exec_distributed_sql_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_DISTRIBUTED_SQL_REQUESTS_TSQL
- SYS.DM_EXEC_DISTRIBUTED_SQL_REQUESTS_TSQL
- DM_EXEC_DISTRIBUTED_SQL_REQUESTS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- sys.dm_exec_distributed_requests management view
- dm_exec_distributed_requests management view
ms.assetid: d065dc01-35d4-472f-9554-53ac41e7d104
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 57f0c150c6c332a7215ef1631c0402488ad7982b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472817"
---
# <a name="sysdm_exec_distributed_sql_requests-transact-sql"></a>sys.dm_exec_distributed_sql_requests (Transact-SQL)
[!INCLUDE [sqlserver2016-asdbmi-asa-pdw](../../includes/applies-to-version/sqlserver2016-asdbmi-asa-pdw.md)]

  Contém informações sobre todas as distribuições de consultas SQL como parte de uma etapa SQL na consulta.  Esta exibição mostra os dados das últimas 1000 solicitações; as solicitações ativas sempre têm os dados presentes nessa exibição.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|execution_id e step_index compõem a chave para essa exibição. ID numérica exclusiva associada à solicitação.|Consulte a ID em [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|  
|step_index|**int**|Índice da etapa de consulta da qual essa distribuição faz parte.|Consulte step_index em [sys.dm_exec_distributed_request_steps &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md).|  
|compute_node_id|**int**|Tipo da operação representada por esta etapa.|Consulte compute_node_id em [sys.dm_exec_compute_nodes &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|distribution_id|**int**|Onde a etapa está em execução.|Defina como-1 para solicitações que são executadas no escopo do nó, não no escopo de distribuição.|  
|status|**nvarchar(32)**|Status desta etapa|Ativo, cancelado, concluído, com falha, na fila|  
|error_id|**nvarchar (36)**|ID exclusiva do erro associado a esta etapa, se houver|Consulte ID de [sys.dm_exec_compute_node_errors &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md), NULL se não ocorreu nenhum erro.|  
|start_time|**datetime**|Hora em que a execução da etapa foi iniciada|Menor ou igual à hora atual e maior ou igual a end_compile_time da consulta à qual essa etapa pertence.|  
|end_time|**datetime**|A hora em que esta etapa concluiu a execução, foi cancelada ou falhou.|Menor ou igual à hora atual e maior ou igual a start_time, definido como nulo para as etapas atualmente em execução ou na fila.|  
|total_elapsed_time|**int**|Quantidade total de tempo que a etapa de consulta foi executada, em milissegundos|Entre 0 e a diferença entre end_time e start_time. 0 para etapas em fila.|  
|row_count|**bigint**|Número total de linhas alteradas ou retornadas por esta solicitação|0 para etapas que não mudaram ou retornarem dados, o número de linhas afetadas de outra forma. Defina como-1 para as etapas de DMS.|  
|spid|**int**|ID da sessão na instância de SQL Server executando a distribuição de consulta||  
|.|nvarchar(4000)|Mantém o texto completo do comando desta etapa.|Qualquer cadeia de caracteres de solicitação válida para uma etapa. Truncado se tiver mais de 4000 caracteres.|  
  
## <a name="see-also"></a>Consulte Também  
 [Solução de problemas do polybase com exibições de gerenciamento dinâmico](/previous-versions/sql/sql-server-2016/mt146389(v=sql.130))   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas ao banco de dados &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
