---
title: sys.dm_exec_query_resource_semaphores (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_query_resource_semaphores_TSQL
- dm_exec_query_resource_semaphores_TSQL
- sys.dm_exec_query_resource_semaphores
- dm_exec_query_resource_semaphores
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_resource_semaphores dynamic management view
ms.assetid: e43a2aa9-dd52-4c89-911e-1a7d05f7ffbb
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3b5fc27e9a6138c3955871d084b62144bda006cd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmexecqueryresourcesemaphores-transact-sql"></a>sys.dm_exec_query_resource_semaphores (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna as informações sobre o status de semáforo do recurso de consulta atual no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. **sys.DM exec_query_resource_semaphores** fornece o status da memória de execução de consulta geral e permite que você determine se o sistema pode acessar memória suficiente. Essa exibição complementa as informações de memória obtidas [sys.DM os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md) para fornecer uma visão completa de status de memória do servidor. **sys.DM exec_query_resource_semaphores** retorna uma linha para o sinal do recurso normal e outra linha para o sinal do recurso de consulta. Há dois requisitos para um sinal de consulta:  
  
-   A concessão de memória solicitada deve ser menor que 5 MB  
  
-   O custo da consulta deve ser menor que 3 unidades de custo  
  
> [!NOTE]  
>  Para chamar essa de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_exec_query_resource_semaphores**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**resource_semaphore_id**|**smallint**|ID não exclusivo do sinal do recurso. 0 para o sinal do recurso normal e 1 para o sinal do recurso da consulta pequena.|  
|**target_memory_kb**|**bigint**|Conceda o destino de uso em quilobytes.|  
|**max_target_memory_kb**|**bigint**|Destino potencial máximo em quilobytes. NULL para o sinal do recurso da consulta pequena.|  
|**total_memory_kb**|**bigint**|Memória usada pelo sinal do recurso em quilobytes. Se o sistema está sob pressão de memória ou se mínima forçada memória é concedida com frequência, esse valor pode ser maior do que o **target_memory_kb** ou **max_target_memory_kb** valores. A memória total é uma soma das memórias disponível e concedida.|  
|**available_memory_kb**|**bigint**|Memória disponível para uma concessão nova em quilobytes.|  
|**granted_memory_kb**|**bigint**|Total de memória concedida em quilobytes.|  
|**used_memory_kb**|**bigint**|Parte fisicamente usada da memória concedida em quilobytes.|  
|**grantee_count**|**Int**|Número de consultas ativas com concessões atendidas.|  
|**waiter_count**|**Int**|Número de consultas que esperam as concessões serem atendidas.|  
|**timeout_error_count**|**bigint**|Número total de erros de tempo-limite desde a inicialização do servidor. NULL para o sinal do recurso da consulta pequena.|  
|**forced_grant_count**|**bigint**|Número total de concessões de memória mínimas forçadas desde a inicialização do servidor. NULL para o sinal do recurso da consulta pequena.|  
|**pool_id**|**Int**|ID do pool de recursos ao qual pertence este sinal do recurso.|  
|**pdw_node_id**|**Int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões  

Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` no banco de dados.   
  
## <a name="remarks"></a>Remarks  
 As consultas que usam exibições de gerenciamento dinâmico com ORDER BY ou agregações podem aumentar o uso da memória e, dessa forma, contribuir para o problema que estão solucionando.  
  
 Use **sys.DM exec_query_resource_semaphores** para solução de problemas, mas não o inclua em aplicativos que utilizarão versões futuras do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O recurso Administrador de Recursos permite que um administrador de banco de dados distribua recursos de servidor entre pools de recursos, até um máximo de 64 pools. No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versões posteriores, cada pool se comporta como uma instância de servidor independente pequena e requer dois semáforos.  
  
## <a name="see-also"></a>Consulte também  
 [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_query_memory_grants &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)  
  
  


