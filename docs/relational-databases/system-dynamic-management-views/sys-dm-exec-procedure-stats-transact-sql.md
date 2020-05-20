---
title: sys. dm_exec_procedure_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_procedure_stats_TSQL
- dm_exec_procedure_stats_TSQL
- dm_exec_procedure_stats
- sys.dm_exec_procedure_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_procedure_stats dynamic management view
ms.assetid: ab8ddde8-1cea-4b41-a7e4-697e6ddd785a
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a3620efe22d2a285aed7f78f6573bdc2280be47f
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829420"
---
# <a name="sysdm_exec_procedure_stats-transact-sql"></a>sys.dm_exec_procedure_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna estatísticas de desempenho de agregação para procedimentos armazenados em cache. A exibição retorna uma linha para cada plano de procedimento armazenado, e o tempo de vida da linha é igual ao tempo em que o procedimento armazenado permanece em cache. Quando um procedimento armazenado é removido do cache, a linha correspondente é eliminada da exibição. Nesse momento, é gerado um evento de Rastreamento do SQL de Estatísticas de Desempenho similar a **sys.dm_exec_query_stats**.  
  
 No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], as exibições de gerenciamento dinâmico não podem expor informações que afetarão a contenção do banco de dados ou informações sobre outros bancos de dados aos quais o usuário tem acesso. Para evitar a exposição dessas informações, todas as linhas que contêm dados que não pertencem ao locatário conectado serão filtradas.  
  
> [!NOTE]
> Os resultados de **Sys. dm_exec_procedure_stats** podem variar com cada execução, já que os dados refletem apenas as consultas concluídas e não os que ainda estão em andamento.
> Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use o nome **Sys. dm_pdw_nodes_exec_procedure_stats**. 

  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------| 
|**database_id**|**int**|ID do banco de dados no qual o procedimento armazenado reside.|  
|**object_id**|**int**|Número de identificação de objeto do procedimento armazenado.|  
|**tipo**|**char(2)**|Tipo do objeto:<br /><br /> P = Procedimento armazenado SQL<br /><br /> PC = Procedimento armazenado de assembly (CLR)<br /><br /> X = Procedimento armazenado estendido|  
|**type_desc**|**nvarchar(60)**|Descrição do tipo de objeto:<br /><br /> SQL_STORED_PROCEDURE<br /><br /> CLR_STORED_PROCEDURE<br /><br /> EXTENDED_STORED_PROCEDURE|  
|**sql_handle**|**varbinary(64)**|Isso pode ser usado para correlacionar com consultas em **Sys. dm_exec_query_stats** que foram executadas de dentro deste procedimento armazenado.|  
|**plan_handle**|**varbinary(64)**|Identificador do plano na memória. Esse identificador é transitório e permanece constante somente enquanto o plano permanece no cache. Esse valor pode ser usado com a exibição de gerenciamento dinâmico **Sys. dm_exec_cached_plans** .<br /><br /> Sempre será 0x000 quando um procedimento armazenado compilado nativamente consultar uma tabela com otimização de memória.|  
|**cached_time**|**datetime**|Hora em que o procedimento armazenado foi adicionado ao cache.|  
|**last_execution_time**|**datetime**|Hora em que o procedimento armazenado foi executado pela última vez.|  
|**execution_count**|**bigint**|O número de vezes que o procedimento armazenado foi executado desde a última compilação.|  
|**total_worker_time**|**bigint**|A quantidade total de tempo de CPU, em microssegundos, que foi consumida por execuções deste procedimento armazenado desde que ele foi compilado.<br /><br /> Para procedimentos armazenados compilados de modo nativo, o **total_worker_time** pode não ser preciso se várias execuções levarem menos de 1 milissegundo.|  
|**last_worker_time**|**bigint**|Tempo de CPU, em microssegundos, consumido na última vez em que o procedimento armazenado foi executado. <sup>1</sup>|  
|**min_worker_time**|**bigint**|O tempo mínimo de CPU, em microssegundos, que esse procedimento armazenado já consumiu durante uma única execução. <sup>1</sup>|  
|**max_worker_time**|**bigint**|O tempo máximo de CPU, em microssegundos, que esse procedimento armazenado já consumiu durante uma única execução. <sup>1</sup>|  
|**total_physical_reads**|**bigint**|O número total de leituras físicas realizadas por execuções deste procedimento armazenado desde que ele foi compilado.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**last_physical_reads**|**bigint**|O número de leituras físicas efetuadas na última vez em que o procedimento armazenado foi executado.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**min_physical_reads**|**bigint**|O número mínimo de leituras físicas que este procedimento armazenado fez durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**max_physical_reads**|**bigint**|O número máximo de leituras físicas que este procedimento armazenado fez durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**total_logical_writes**|**bigint**|O número total de gravações lógicas realizadas por execuções deste procedimento armazenado desde que ele foi compilado.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**last_logical_writes**|**bigint**|O número de páginas do pool de buffers sujos na última vez em que o plano foi executado. Se uma página já estiver suja (modificada), nenhuma gravação será contabilizada.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**min_logical_writes**|**bigint**|O número mínimo de gravações lógicas que esse procedimento armazenado fez durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**max_logical_writes**|**bigint**|O número máximo de gravações lógicas que esse procedimento armazenado fez durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**total_logical_reads**|**bigint**|O número total de leituras lógicas realizadas por execuções deste procedimento armazenado desde que ele foi compilado.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**last_logical_reads**|**bigint**|O número de leituras lógicas efetuadas na última vez em que o procedimento armazenado foi executado.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**min_logical_reads**|**bigint**|O número mínimo de leituras lógicas que esse procedimento armazenado fez durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**max_logical_reads**|**bigint**|O número máximo de leituras lógicas que esse procedimento armazenado fez durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**total_elapsed_time**|**bigint**|O tempo total decorrido, em microssegundos, para execuções concluídas desse procedimento armazenado.|  
|**last_elapsed_time**|**bigint**|O tempo decorrido, em microssegundos, para a execução concluída mais recentemente desse procedimento armazenado.|  
|**min_elapsed_time**|**bigint**|O tempo mínimo decorrido, em microssegundos, para qualquer execução concluída desse procedimento armazenado.|  
|**max_elapsed_time**|**bigint**|O tempo máximo decorrido, em microssegundos, para qualquer execução concluída desse procedimento armazenado.|  
|**total_spills**|**bigint**|O número total de páginas despejadas pela execução deste procedimento armazenado desde que ele foi compilado.<br /><br /> **Aplica-se a: a**partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] Cu3|  
|**last_spills**|**bigint**|O número de páginas despejadas na última vez em que o procedimento armazenado foi executado.<br /><br /> **Aplica-se a: a**partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] Cu3|  
|**min_spills**|**bigint**|O número mínimo de páginas que esse procedimento armazenado já excedeu durante uma única execução.<br /><br /> **Aplica-se a: a**partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] Cu3|  
|**max_spills**|**bigint**|O número máximo de páginas que esse procedimento armazenado já excedeu durante uma única execução.<br /><br /> **Aplica-se a: a**partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] Cu3|  
|**pdw_node_id**|**int**|O identificador do nó em que essa distribuição está.<br /><br />**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
|**total_page_server_reads**|**bigint**|O número total de leituras de servidor de página executadas por execuções deste procedimento armazenado desde que ele foi compilado.<br /><br /> **Aplica-se a**: hiperescala do banco de dados SQL do Azure|  
|**last_page_server_reads**|**bigint**|O número de leituras do servidor de página executadas na última vez em que o procedimento armazenado foi executado.<br /><br /> **Aplica-se a**: hiperescala do banco de dados SQL do Azure|  
|**min_page_server_reads**|**bigint**|O número mínimo de leituras do servidor de páginas que esse procedimento armazenado já realizou durante uma única execução.<br /><br /> **Aplica-se a**: hiperescala do banco de dados SQL do Azure|  
|**max_page_server_reads**|**bigint**|O número máximo de páginas de servidor de página que esse procedimento armazenado já realizou durante uma única execução.<br /><br /> **Aplica-se a**: hiperescala do banco de dados SQL do Azure|  
  
 <sup>1</sup> para procedimentos armazenados compilados nativamente quando a coleta de estatísticas está habilitada, o tempo de trabalho é coletado em milissegundos. Se a consulta for executada em menos de um milissegundo, o valor será 0.  
  
## <a name="permissions"></a>Permissões  

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a `VIEW DATABASE STATE` permissão no banco de dados. Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   
   
## <a name="remarks"></a>Comentários  
 As estatísticas da exibição serão atualizadas quando uma execução de procedimento armazenado for concluída.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações sobre os dez principais procedimentos armazenados identificados por tempo médio decorrido.  
  
```sql  
SELECT TOP 10 d.object_id, d.database_id, OBJECT_NAME(object_id, database_id) 'proc name',   
    d.cached_time, d.last_execution_time, d.total_elapsed_time,  
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],  
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_procedure_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>Consulte Também  
[Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
[sys. dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
[sys. dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)    
[sys. dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)    
[sys. dm_exec_trigger_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)    
[sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)    
  
  


