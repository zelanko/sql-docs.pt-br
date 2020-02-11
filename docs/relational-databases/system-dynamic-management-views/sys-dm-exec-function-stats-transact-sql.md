---
title: sys. dm_exec_function_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/30/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_function_stats
- sys.dm_exec_function_stats_tsql
- dm_exec_function_stats
- dm_exec_function_stats_tsql
helpviewer_keywords:
- sys.dm_exec_function_stats dynamic management view
ms.assetid: 4c3d6a02-08e4-414b-90be-36b89a0e5a3a
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 89d66217536d5cd552eb11de67d6d97d21ec9f6e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68742830"
---
# <a name="sysdm_exec_function_stats-transact-sql"></a>sys. dm_exec_function_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Retorna estatísticas de desempenho agregadas para funções armazenadas em cache. A exibição retorna uma linha para cada plano de função em cache e o tempo de vida da linha é desde que a função permaneça armazenada em cache. Quando uma função é removida do cache, a linha correspondente é eliminada dessa exibição. Nesse momento, é gerado um evento de Rastreamento do SQL de Estatísticas de Desempenho similar a **sys.dm_exec_query_stats**. Retorna informações sobre funções escalares, incluindo funções na memória e funções escalares CLR. Não retorna informações sobre funções com valor de tabela.  
  
 No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], as exibições de gerenciamento dinâmico não podem expor informações que afetarão a contenção do banco de dados ou informações sobre outros bancos de dados aos quais o usuário tem acesso. Para evitar a exposição dessas informações, todas as linhas que contêm dados que não pertencem ao locatário conectado serão filtradas.  
  
> [!NOTE]
> Os resultados de **Sys. dm_exec_function_stats** podem variar com cada execução, já que os dados refletem apenas as consultas concluídas e não os que ainda estão em andamento. 

  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|A ID do banco de dados na qual a função reside.|  
|**object_id**|**int**|Número de identificação do objeto da função.|  
|**tipo**|**Char (2)**|Tipo do objeto: FN = funções com valor escalar|  
|**type_desc**|**nvarchar (60)**|Descrição do tipo de objeto: SQL_SCALAR_FUNCTION|  
|**sql_handle**|**varbinary (64)**|Isso pode ser usado para correlacionar com consultas em **Sys. dm_exec_query_stats** que foram executadas de dentro dessa função.|  
|**plan_handle**|**varbinary (64)**|Identificador do plano na memória. Esse identificador é transitório e permanece constante somente enquanto o plano permanece no cache. Esse valor pode ser usado com a exibição de gerenciamento dinâmico **Sys. dm_exec_cached_plans** .<br /><br /> Sempre será 0x000 quando uma função compilada nativamente consultar uma tabela com otimização de memória.|  
|**cached_time**|**datetime**|Hora em que a função foi adicionada ao cache.|  
|**last_execution_time**|**datetime**|Última vez em que a função foi executada.|  
|**execution_count**|**bigint**|Número de vezes que a função foi executada desde a última compilação.|  
|**total_worker_time**|**bigint**|Quantidade total de tempo de CPU, em microssegundos, que foi consumida por execuções dessa função desde que ela foi compilada.<br /><br /> Para funções compiladas nativamente, **total_worker_time** pode não ser preciso se muitas execuções demorarem menos de 1 milissegundo.|  
|**last_worker_time**|**bigint**|Tempo de CPU, em microssegundos, que foi consumido na última vez em que a função foi executada. <sup>1</sup>|  
|**min_worker_time**|**bigint**|Tempo mínimo de CPU, em microssegundos, que essa função já consumiu durante uma única execução. <sup>1</sup>|  
|**max_worker_time**|**bigint**|Tempo máximo de CPU, em microssegundos, que essa função já consumiu durante uma única execução. <sup>1</sup>|  
|**total_physical_reads**|**bigint**|Número total de leituras físicas executadas por execuções dessa função desde que ela foi compilada.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**last_physical_reads**|**bigint**|Número de leituras físicas efetuadas na última vez em que a função foi executada.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**min_physical_reads**|**bigint**|Número mínimo de leituras físicas que essa função já realizou durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**max_physical_reads**|**bigint**|Número máximo de leituras físicas que essa função já realizou durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**total_logical_writes**|**bigint**|Número total de gravações lógicas realizadas por execuções dessa função desde que ela foi compilada.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**last_logical_writes**|**bigint**|O número de páginas do pool de buffers que foram sujas na última vez em que o plano foi executado. Se uma página já estiver suja (modificada), nenhuma gravação será contabilizada.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**min_logical_writes**|**bigint**|Número mínimo de gravações lógicas que essa função realizou durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**max_logical_writes**|**bigint**|Número máximo de gravações lógicas que essa função realizou durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**total_logical_reads**|**bigint**|Número total de leituras lógicas realizadas por execuções dessa função desde que ela foi compilada.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**last_logical_reads**|**bigint**|Número de leituras lógicas efetuadas na última vez em que a função foi executada.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**min_logical_reads**|**bigint**|Número mínimo de leituras lógicas que essa função já realizou durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**max_logical_reads**|**bigint**|Número máximo de leituras lógicas que essa função já realizou durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**total_elapsed_time**|**bigint**|Tempo total decorrido, em microssegundos, para execuções concluídas dessa função.|  
|**last_elapsed_time**|**bigint**|Tempo decorrido, em microssegundos, para a execução concluída mais recentemente dessa função.|  
|**min_elapsed_time**|**bigint**|Tempo mínimo decorrido, em microssegundos, para qualquer execução concluída dessa função.|  
|**max_elapsed_time**|**bigint**|Tempo máximo decorrido, em microssegundos, para qualquer execução concluída dessa função.|  
|**total_page_server_reads**|**bigint**|Número total de leituras de servidor de página executadas por execuções dessa função desde que ela foi compilada.<br /><br /> **Aplica-se a:** Hiperescala do banco de dados SQL do Azure.|  
|**last_page_server_reads**|**bigint**|Número de leituras do servidor de páginas executadas na última vez em que a função foi executada.<br /><br /> **Aplica-se a:** Hiperescala do banco de dados SQL do Azure.|  
|**min_page_server_reads**|**bigint**|O número mínimo de leituras de servidor de página que essa função já realizou durante uma única execução.<br /><br /> **Aplica-se a:** Hiperescala do banco de dados SQL do Azure.|  
|**max_page_server_reads**|**bigint**|O número máximo de leituras de servidor de página que essa função já realizou durante uma única execução.<br /><br /> **Aplica-se a:** Hiperescala do banco de dados SQL do Azure.|
  
## <a name="permissions"></a>Permissões  

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a `VIEW DATABASE STATE` permissão no banco de dados. Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações sobre as dez funções principais identificadas por tempo médio decorrido.  
  
```  
SELECT TOP 10 d.object_id, d.database_id, OBJECT_NAME(object_id, database_id) 'function name',   
    d.cached_time, d.last_execution_time, d.total_elapsed_time,  
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],  
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_function_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys. dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 
 [sys. dm_exec_trigger_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)   
 [sys. dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  
  
  
