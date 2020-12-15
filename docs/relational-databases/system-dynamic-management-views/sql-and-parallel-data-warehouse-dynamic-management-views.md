---
description: Exibições de gerenciamento dinâmico do SQL e Parallel data warehouse
title: Exibições de gerenciamento dinâmico do SQL e Parallel data warehouse
ms.custom: seo-dt-2019
ms.date: 11/05/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: julieMSFT
ms.author: jrasnick
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: e1735fa9e8b8ad6a85648b21aab1ba9aa21062b2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97466877"
---
# <a name="sql-and-parallel-data-warehouse-dynamic-management-views"></a>Exibições de gerenciamento dinâmico do SQL e Parallel data warehouse
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

Este tópico lista as [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] DMVs (exibições de gerenciamento dinâmico).  
  
 Todos [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] DMVs começam com **Sys.dm_pdw**.  
  
## <a name="sssdw-and-sspdw-dynamic-management-views"></a>[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] exibições de gerenciamento dinâmico  
 As exibições de gerenciamento dinâmico a seguir se aplicam ao [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e ao [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] :  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_dms_cores ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-cores-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_dms_external_work ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-external-work-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_dms_workers ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_errors ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_exec_connections ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-connections-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_exec_requests ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_exec_sessions ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_hadoop_operations ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-hadoop-operations-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_lock_waits ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_nodes ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_nodes_database_encryption_keys ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_os_threads ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-os-threads-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_request_steps ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_resource_waits ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_sql_requests ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-sql-requests-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_sys_info ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-sys-info-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_wait_stats ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-wait-stats-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_waits ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)

## <a name="sssdw-dynamic-management-views"></a>[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Exibições de gerenciamento dinâmico 
 As exibições de gerenciamento dinâmico a seguir se aplicam [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] somente a:
 
[&#41;&#40;Transact-SQL de sys.dm_pdw_nodes_exec_query_plan ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-exec-query-plan-transact-sql.md)  

[&#41;&#40;Transact-SQL de sys.dm_pdw_nodes_exec_query_profiles ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-exec-query-profiles-transact-sql.md)  

[&#41;&#40;Transact-SQL de sys.dm_pdw_nodes_exec_query_statistics_xml ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-exec-query-statistics-xml-transact-sql.md)  

[&#41;de &#40;de texto de sys.dm_pdw_nodes_exec_sql de Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-exec-sql-text-transact-sql.md)  

[&#41;&#40;Transact-SQL de sys.dm_pdw_nodes_exec_text_query_plan ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-exec-text-query-plan-transact-sql.md)

 [&#41;de &#40;Transact-SQL de sys.dm_workload_management_workload_groups_stats ](../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md) (versão prévia)

## <a name="sspdw-dynamic-management-views"></a>[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Exibições de gerenciamento dinâmico  
 As exibições de gerenciamento dinâmico a seguir se aplicam [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] somente a:  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_component_health_active_alerts ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_component_health_alerts ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-alerts-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_component_health_status ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_diag_processing_stats ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-diag-processing-stats-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_network_credentials ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_node_status ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-node-status-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_os_event_logs ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-os-event-logs-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_os_performance_counters ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-os-performance-counters-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_query_stats_xe ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-query-stats-xe-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.dm_pdw_query_stats_xe_file ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-query-stats-xe-file-transact-sql.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
