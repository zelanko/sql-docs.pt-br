---
title: sys.dm_exec_distributed_sql_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 09837558489ea2f4ae5c8bc470da01f15d2e4dcf
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmexecdistributedsqlrequests-transact-sql"></a>sys.dm_exec_distributed_sql_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contém informações sobre todas as distribuições de consulta SQL como parte de uma etapa SQL na consulta.  Essa exibição mostra os dados para as últimas 1000 solicitações; solicitações ativas sempre têm os dados presentes nesta exibição.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|execution_id e step_index constituem a chave para este modo de exibição. Id numérico exclusivo associado à solicitação.|Consulte a ID de [exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|  
|step_index|**Int**|Índice da etapa de consulta que essa distribuição é parte do.|Consulte step_index em [sys.dm_exec_distributed_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md).|  
|compute_node_id|**Int**|Tipo de operação representado por essa etapa.|Consulte compute_node_id em [sys.DM exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|distribution_id|**Int**|Onde a etapa está sendo executado.|Definido como -1 para solicitações que são executados no escopo do nó não o escopo de distribuição.|  
|status|**nvarchar(32)**|Status desta etapa|Ativo, cancelado, concluído, com falha, em fila|  
|error_id|**nvarchar(36)**|Id exclusiva do erro associado a essa etapa, se houver|Consulte a id de [sys.dm_exec_compute_node_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md), NULL se nenhum erro ocorreu.|  
|start_time|**datetime**|Hora em que a etapa iniciou a execução|Menor ou igual à hora atual e maior ou igual a end_compile_time da consulta ao qual pertence essa etapa.|  
|end_time|**datetime**|Hora em que esta etapa concluiu a execução, foi cancelada ou falha.|Menor ou igual à hora atual e maior ou igual a start_time, definida como NULL para etapas atualmente em execução ou na fila.|  
|total_elapsed_time|**Int**|Quantidade total de tempo de que execução de etapa de consulta, em milissegundos|Entre 0 e a diferença entre start_time e end_time. 0 para etapas em fila.|  
|row_count|**bigint**|Número total de linhas alteradas ou retornado por esta solicitação|0 para as etapas que não alterar ou retornar dados, o número de linhas afetadas caso contrário. Defina como -1 para etapas DMS.|  
|spid|**Int**|Id da sessão na instância do SQL Server executando a distribuição de consulta||  
|command|nvarchar(4000)|Contém o texto completo do comando desta etapa.|Qualquer cadeia de caracteres de solicitação válida para uma etapa. Truncado se mais de 4000 caracteres.|  
  
## <a name="see-also"></a>Consulte também  
 [PolyBase, solucionando problemas com exibições de gerenciamento dinâmico](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Banco de dados relacionados a exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
