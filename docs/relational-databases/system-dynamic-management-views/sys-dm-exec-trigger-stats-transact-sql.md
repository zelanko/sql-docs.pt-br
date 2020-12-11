---
description: sys.dm_exec_trigger_stats (Transact-SQL)
title: sys.dm_exec_trigger_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_trigger_stats
- dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_trigger_stats dynamic management function
ms.assetid: 863498b4-849c-434d-b748-837411458738
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 51a83d1a812df700c2685598498312ee6b29bde0
ms.sourcegitcommit: 2991ad5324601c8618739915aec9b184a8a49c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97334142"
---
# <a name="sysdm_exec_trigger_stats-transact-sql"></a>sys.dm_exec_trigger_stats (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna estatísticas de desempenho de agregação dos gatilhos em cache. A exibição contém uma linha por gatilho e o tempo de vida da linha equivale ao tempo de permanência do gatilho em cache. Quando um gatilho é removido do cache, a linha correspondente é eliminada desta exibição. Nesse momento, é gerado um evento de Rastreamento do SQL de Estatísticas de Desempenho similar a **sys.dm_exec_query_stats**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID do banco de dados no qual o gatilho reside.|  
|**object_id**|**int**|Número de identificação de objeto do gatilho.|  
|**tipo**|**char(2)**|Tipo do objeto:<br /><br /> TA = Gatilho (CLR) de assembly<br /><br /> TR = Gatilho SQL|  
|**Type_desc**|**nvarchar(60)**|Descrição do tipo de objeto:<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**sql_handle**|**varbinary(64)**|Isso pode ser usado para correlacionar com consultas no **Sys.dm_exec_query_stats** que foram executadas a partir desse gatilho.|  
|**plan_handle**|**varbinary(64)**|Identificador do plano na memória. Esse identificador é transitório e permanece constante somente enquanto o plano permanece no cache. Esse valor pode ser usado com a exibição de gerenciamento dinâmico **Sys.dm_exec_cached_plans** .|  
|**cached_time**|**datetime**|Hora em que o gatilho foi adicionado ao cache.|  
|**last_execution_time**|**datetime**|Hora da última execução do gatilho.|  
|**execution_count**|**bigint**|O número de vezes que o gatilho foi executado desde a última compilação.|  
|**total_worker_time**|**bigint**|A quantidade total de tempo de CPU, em microssegundos, que foi consumida por execuções desse gatilho desde que ele foi compilado.|  
|**last_worker_time**|**bigint**|Tempo de CPU, em microssegundos, consumido na última vez em que o gatilho foi executado.|  
|**min_worker_time**|**bigint**|O tempo máximo de CPU, em microssegundos, que esse gatilho já consumiu durante uma única execução.|  
|**max_worker_time**|**bigint**|O tempo máximo de CPU, em microssegundos, que esse gatilho já consumiu durante uma única execução.|  
|**total_physical_reads**|**bigint**|O número total de leituras físicas executadas por execuções deste gatilho desde sua compilação.|  
|**last_physical_reads**|**bigint**|O número de leituras físicas efetuadas na última vez em que o gatilho foi executado.|  
|**min_physical_reads**|**bigint**|O número mínimo de leituras físicas que esse gatilho fez durante uma única execução.|  
|**max_physical_reads**|**bigint**|O número máximo de leituras físicas que esse gatilho fez durante uma única execução.|  
|**total_logical_writes**|**bigint**|O número total de gravações lógicas realizadas por execuções deste gatilho desde sua compilação.|  
|**last_logical_writes**|**bigint**|O número de gravações lógicas realizadas na última vez em que o gatilho foi executado.|  
|**min_logical_writes**|**bigint**|O número mínimo de gravações lógicas que esse gatilho fez durante uma única execução.|  
|**max_logical_writes**|**bigint**|O número máximo de gravações lógicas que esse gatilho fez durante uma única execução.|  
|**total_logical_reads**|**bigint**|O número total de leituras lógicas realizadas por execuções deste gatilho desde sua compilação.|  
|**last_logical_reads**|**bigint**|O número de leituras lógicas efetuadas na última vez em que o gatilho foi executado.|  
|**min_logical_reads**|**bigint**|O número mínimo de leituras lógicas que esse gatilho fez durante uma única execução.|  
|**max_logical_reads**|**bigint**|O número máximo de leituras lógicas que esse gatilho fez durante uma única execução.|  
|**total_elapsed_time**|**bigint**|O tempo total decorrido, em microssegundos, para execuções concluídas desse gatilho.|  
|**last_elapsed_time**|**bigint**|Tempo decorrido, em microssegundos, da execução concluída mais recente deste gatilho.|  
|**min_elapsed_time**|**bigint**|O tempo mínimo decorrido, em microssegundos, para qualquer execução concluída desse gatilho.|  
|**max_elapsed_time**|**bigint**|O tempo máximo decorrido, em microssegundos, para qualquer execução concluída desse gatilho.| 
|**total_spills**|**bigint**|O número total de páginas despejadas pela execução deste gatilho desde sua compilação.<br /><br /> **Aplica-se a: a** partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] Cu3|  
|**last_spills**|**bigint**|O número de páginas despejadas na última vez em que o gatilho foi executado.<br /><br /> **Aplica-se a: a** partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] Cu3|  
|**min_spills**|**bigint**|O número mínimo de páginas que esse gatilho já excedeu durante uma única execução.<br /><br /> **Aplica-se a: a** partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] Cu3|  
|**max_spills**|**bigint**|O número máximo de páginas que esse gatilho já excedeu durante uma única execução.<br /><br /> **Aplica-se a: a** partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] Cu3|  
|**total_page_server_reads**|**bigint**|O número total de leituras de servidor de página executadas por execuções deste gatilho desde sua compilação.<br /><br /> **Aplica-se a**: hiperescala do banco de dados SQL do Azure|  
|**last_page_server_reads**|**bigint**|O número de leituras do servidor de página realizadas na última vez em que o gatilho foi executado.<br /><br /> **Aplica-se a**: hiperescala do banco de dados SQL do Azure|  
|**min_page_server_reads**|**bigint**|O número mínimo de leituras de servidor de página que esse gatilho já realizou durante uma única execução.<br /><br /> **Aplica-se a**: hiperescala do banco de dados SQL do Azure|  
|**max_page_server_reads**|**bigint**|O número máximo de páginas de servidor de página que esse gatilho já realizou durante uma única execução.<br /><br /> **Aplica-se a**: hiperescala do banco de dados SQL do Azure|  

  
## <a name="remarks"></a>Comentários  
 No [!INCLUDE[ssSDS](../../includes/sssds-md.md)], as exibições de gerenciamento dinâmico não podem expor informações que afetarão a contenção do banco de dados ou informações sobre outros bancos de dados aos quais o usuário tem acesso. Para evitar a exposição dessas informações, todas as linhas que contêm dados que não pertencem ao locatário conectado serão filtradas.  

As estatísticas na exibição são atualizadas quando uma consulta é concluída.  
  
## <a name="permissions"></a>Permissões  

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nos objetivos do serviço básico, S0 e S1 do banco de dados SQL, e para bancos de dados em pools elásticos, o `Server admin` ou uma `Azure Active Directory admin` conta é necessária. Em todos os outros objetivos de serviço do banco de dados SQL, a `VIEW DATABASE STATE` permissão é necessária no banco de dados.   
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações sobre os cinco principais gatilhos identificados por tempo médio decorrido.  
  
```sql  
SELECT TOP 5 d.object_id, d.database_id, DB_NAME(database_id) AS 'database_name',   
    OBJECT_NAME(object_id, database_id) AS 'trigger_name', d.cached_time,  
    d.last_execution_time, d.total_elapsed_time,   
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],   
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_trigger_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>Consulte Também  
[Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
[&#41;&#40;Transact-SQL de sys.dm_exec_sql_text ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
[&#41;&#40;Transact-SQL de sys.dm_exec_query_stats ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
[&#41;&#40;Transact-SQL de sys.dm_exec_procedure_stats ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)   
[sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
  
