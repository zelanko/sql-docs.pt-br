---
title: exec_trigger_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_exec_trigger_stats
- dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_trigger_stats dynamic management function
ms.assetid: 863498b4-849c-434d-b748-837411458738
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 67c6d5765ee5259134f6d9985a88bf94768490cf
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexectriggerstats-transact-sql"></a>sys.dm_exec_trigger_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna estatísticas de desempenho de agregação dos gatilhos em cache. A exibição contém uma linha por gatilho e o tempo de vida da linha equivale ao tempo de permanência do gatilho em cache. Quando um gatilho é removido do cache, a linha correspondente é eliminada desta exibição. Nesse momento, um evento de rastreamento de SQL de estatísticas de desempenho é gerado como **sys.DM exec_query_stats**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID do banco de dados no qual o gatilho reside.|  
|**object_id**|**int**|Número de identificação de objeto do gatilho.|  
|**tipo**|**char(2)**|Tipo do objeto:<br /><br /> TA = Gatilho (CLR) de assembly<br /><br /> TR = Gatilho SQL|  
|**Type_desc**|**nvarchar (60)**|Descrição do tipo de objeto:<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**sql_handle**|**varbinary(64)**|Isso pode ser usado para correlacionar com as consultas de **sys.DM exec_query_stats** que foram executadas a partir deste gatilho.|  
|**plan_handle**|**varbinary(64)**|Identificador do plano na memória. Esse identificador é transitório e permanece constante somente enquanto o plano permanece no cache. Esse valor pode ser usado com o **exec_cached_plans** exibição de gerenciamento dinâmico.|  
|**cached_time**|**datetime**|Hora em que o gatilho foi adicionado ao cache.|  
|**last_execution_time**|**datetime**|Hora da última execução do gatilho.|  
|**execution_count**|**bigint**|Número de vezes que o gatilho foi executado desde sua última compilação.|  
|**total_worker_time**|**bigint**|Tempo total de CPU, em microssegundos, consumido por execuções deste gatilho desde sua compilação.|  
|**last_worker_time**|**bigint**|Tempo de CPU, em microssegundos, consumido na última vez em que o gatilho foi executado.|  
|**min_worker_time**|**bigint**|Tempo máximo de CPU, em microssegundos, que este gatilho consumiu durante uma única execução.|  
|**max_worker_time**|**bigint**|Tempo máximo de CPU, em microssegundos, que este gatilho consumiu durante uma única execução.|  
|**total_physical_reads**|**bigint**|Número total de leituras físicas efetuadas por execuções deste gatilho desde sua compilação.|  
|**last_physical_reads**|**bigint**|Número de leituras físicas efetuadas na última vez em que o gatilho foi executado.|  
|**min_physical_reads**|**bigint**|Número mínimo de leituras físicas que este gatilho efetuou durante uma única execução.|  
|**max_physical_reads**|**bigint**|Número máximo de leituras físicas que este gatilho efetuou durante uma única execução.|  
|**total_logical_writes**|**bigint**|Número total de gravações lógicas efetuadas por execuções deste gatilho desde sua compilação.|  
|**last_logical_writes**|**bigint**|**total_physical_reads**número de gravações lógicas efetuadas na última vez em que o gatilho foi executado.|  
|**min_logical_writes**|**bigint**|Número mínimo de gravações lógicas que este gatilho efetuou durante uma única execução.|  
|**max_logical_writes**|**bigint**|Número máximo de gravações lógicas que este gatilho efetuou durante uma única execução.|  
|**total_logical_reads**|**bigint**|Número total de leituras lógicas efetuadas por execuções deste gatilho desde sua compilação.|  
|**last_logical_reads**|**bigint**|Número de leituras lógicas efetuadas na última vez em que o gatilho foi executado.|  
|**min_logical_reads**|**bigint**|Número mínimo de leituras lógicas que este gatilho efetuou durante uma única execução.|  
|**max_logical_reads**|**bigint**|Número máximo de leituras lógicas que este gatilho efetuou durante uma única execução.|  
|**total_elapsed_time**|**bigint**|Tempo decorrido total, em microssegundos, de execuções concluídas deste gatilho.|  
|**last_elapsed_time**|**bigint**|Tempo decorrido, em microssegundos, da execução concluída mais recente deste gatilho.|  
|**min_elapsed_time**|**bigint**|Tempo mínimo decorrido, em microssegundos, de qualquer execução concluída deste gatilho.|  
|**max_elapsed_time**|**bigint**|Tempo máximo decorrido, em microssegundos, de qualquer execução concluída deste gatilho.|  
  
## <a name="remarks"></a>Comentários  
 No Banco de Dados SQL do Windows Azure, as exibições de gerenciamento dinâmico não podem expor informações que afetarão a contenção do banco de dados ou informações sobre outros bancos de dados aos quais o usuário tem acesso. Para evitar a exposição dessas informações, cada linha que contém os dados que não pertencem ao locatário conectado será filtrada.  

As estatísticas na exibição são atualizadas quando uma consulta é concluída.  
  
## <a name="permissions"></a>Permissões  
Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, requer o `VIEW DATABASE STATE` no banco de dados. Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, requer o **administrador do servidor** ou um **administrador do Active Directory do Azure** conta.
  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações sobre os cinco principais gatilhos identificados por tempo médio decorrido.  
  
```sql  
PRINT '--top 5 CPU consuming triggers '  
  
SELECT TOP 5 d.object_id, d.database_id, DB_NAME(database_id) AS 'database_name',   
    OBJECT_NAME(object_id, database_id) AS 'trigger_name', d.cached_time,  
    d.last_execution_time, d.total_elapsed_time,   
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],   
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_trigger_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções e exibições de gerenciamento dinâmico &#40; relacionadas à execução Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.DM exec_sql_text &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.DM exec_query_stats &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
  [sys.DM exec_procedure_stats &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)   
 [exec_cached_plans &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
  
