---
title: sys.DM exec_procedure_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/10/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_procedure_stats_TSQL
- dm_exec_procedure_stats_TSQL
- dm_exec_procedure_stats
- sys.dm_exec_procedure_stats
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_procedure_stats dynamic management view
ms.assetid: ab8ddde8-1cea-4b41-a7e4-697e6ddd785a
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: f8e20e1ebf036e61585f2a690452354de2ba3f71
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/12/2018
---
# <a name="sysdmexecprocedurestats-transact-sql"></a>sys.dm_exec_procedure_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna estatísticas de desempenho de agregação para procedimentos armazenados em cache. A exibição retorna uma linha para cada plano de procedimento armazenado, e o tempo de vida da linha é igual ao tempo em que o procedimento armazenado permanece em cache. Quando um procedimento armazenado é removido do cache, a linha correspondente é eliminada da exibição. Nesse momento, um evento de rastreamento de SQL de estatísticas de desempenho é gerado como **sys.DM exec_query_stats**.  
  
 No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], as exibições de gerenciamento dinâmico não podem expor informações que afetarão a contenção do banco de dados ou informações sobre outros bancos de dados aos quais o usuário tem acesso. Para evitar a exposição dessas informações, cada linha que contém os dados que não pertencem ao locatário conectado será filtrada.  
  
> [!NOTE]
> Uma consulta inicial de **sys.DM exec_procedure_stats** pode produzir resultados inexatos se houver uma carga de trabalho atualmente em execução no servidor. Mais resultados precisos podem ser determinados pela reexecução da consulta.  
  
> [!NOTE]
> Para chamar essa de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_exec_procedure_stats**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**Int**|ID do banco de dados no qual o procedimento armazenado reside.|  
|**object_id**|**Int**|Número de identificação de objeto do procedimento armazenado.|  
|**type**|**char(2)**|Tipo do objeto:<br /><br /> P = procedimento armazenado SQL<br /><br /> PC = Procedimento armazenado de assembly (CLR)<br /><br /> X = Procedimento armazenado estendido|  
|**type_desc**|**nvarchar (60)**|Descrição do tipo de objeto:<br /><br /> SQL_STORED_PROCEDURE<br /><br /> CLR_STORED_PROCEDURE<br /><br /> EXTENDED_STORED_PROCEDURE|  
|**sql_handle**|**varbinary(64)**|Isso pode ser usado para correlacionar com as consultas de **sys.DM exec_query_stats** que foram executadas a partir deste procedimento armazenado.|  
|**plan_handle**|**varbinary(64)**|Identificador do plano na memória. Esse identificador é transitório e permanece constante somente enquanto o plano permanece no cache. Esse valor pode ser usado com o **exec_cached_plans** exibição de gerenciamento dinâmico.<br /><br /> Sempre será 0x000 quando um procedimento armazenado compilado nativamente consultar uma tabela com otimização de memória.|  
|**cached_time**|**datetime**|Hora em que o procedimento armazenado foi adicionado ao cache.|  
|**last_execution_time**|**datetime**|Hora em que o procedimento armazenado foi executado pela última vez.|  
|**execution_count**|**bigint**|O número de vezes que o procedimento armazenado foi executado desde sua última compilação.|  
|**total_worker_time**|**bigint**|A quantidade total de tempo de CPU, em microssegundos, consumido por execuções deste procedimento armazenado desde sua compilação.<br /><br /> Para procedimentos armazenados compilados de modo nativo, o **total_worker_time** pode não ser preciso se várias execuções levarem menos de 1 milissegundo.|  
|**last_worker_time**|**bigint**|Tempo de CPU, em microssegundos, consumido na última vez em que o procedimento armazenado foi executado. <sup>1</sup>|  
|**min_worker_time**|**bigint**|O tempo de CPU mínimo, em microssegundos, que este procedimento armazenado consumiu durante uma única execução. <sup>1</sup>|  
|**max_worker_time**|**bigint**|O tempo máximo de CPU, em microssegundos, que este procedimento armazenado consumiu durante uma única execução. <sup>1</sup>|  
|**total_physical_reads**|**bigint**|O número total de leituras físicas efetuadas por execuções deste procedimento armazenado desde sua compilação.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**last_physical_reads**|**bigint**|O número de leituras físicas efetuadas na última vez em que o procedimento armazenado foi executado.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**min_physical_reads**|**bigint**|O número mínimo de leituras físicas que este procedimento armazenado efetuou durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**max_physical_reads**|**bigint**|O número máximo de leituras físicas que este procedimento armazenado efetuou durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**total_logical_writes**|**bigint**|O número total de gravações lógicas efetuadas por execuções deste procedimento armazenado desde sua compilação.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**last_logical_writes**|**bigint**|O número de páginas de pool de buffer sujas na última vez que o plano foi executado. Se uma página já estiver suja (modificada), nenhuma gravação será contabilizada.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**min_logical_writes**|**bigint**|O número mínimo de gravações lógicas que este procedimento armazenado efetuou durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**max_logical_writes**|**bigint**|O número máximo de gravações lógicas que este procedimento armazenado efetuou durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**total_logical_reads**|**bigint**|O número total de leituras lógicas efetuadas por execuções deste procedimento armazenado desde sua compilação.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**last_logical_reads**|**bigint**|O número de leituras lógicas efetuadas na última vez em que o procedimento armazenado foi executado.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**min_logical_reads**|**bigint**|O número mínimo de leituras lógicas que este procedimento armazenado efetuou durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**max_logical_reads**|**bigint**|O número máximo de leituras lógicas que este procedimento armazenado efetuou durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**total_elapsed_time**|**bigint**|O tempo total decorrido, em microssegundos, de execuções concluídas deste procedimento armazenado.|  
|**last_elapsed_time**|**bigint**|O tempo decorrido, em microssegundos, da execução concluída mais recente deste procedimento armazenado.|  
|**min_elapsed_time**|**bigint**|O tempo mínimo decorrido, em microssegundos, de qualquer execução concluída deste procedimento armazenado.|  
|**max_elapsed_time**|**bigint**|O tempo máximo decorrido, em microssegundos, de qualquer execução concluída deste procedimento armazenado.|  
|**total_spills**|**bigint**|O número total de páginas vazados pela execução deste procedimento armazenado desde sua compilação.<br /><br /> **Aplica-se a**: começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**last_spills**|**bigint**|O número de páginas vazadas a última vez em que o procedimento armazenado foi executado.<br /><br /> **Aplica-se a**: começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**min_spills**|**bigint**|O número mínimo de páginas que este procedimento armazenado já tem vazadas durante uma única execução.<br /><br /> **Aplica-se a**: começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**max_spills**|**bigint**|O número máximo de páginas que este procedimento armazenado já tem vazadas durante uma única execução.<br /><br /> **Aplica-se a**: começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**pdw_node_id**|**Int**|O identificador para o nó que essa distribuição é no.<br /><br />**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
  
 <sup>1</sup> para procedimentos armazenados compilados nativamente quando a coleta de estatísticas é habilitada, o tempo de trabalho será coletado em milissegundos. Se a consulta for executada em menos de um milissegundo, o valor será 0.  
  
## <a name="permissions"></a>Permissões  
Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, requer o `VIEW DATABASE STATE` no banco de dados. Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, requer o **administrador do servidor** ou um **administrador do Active Directory do Azure** conta. 
  
## <a name="remarks"></a>Remarks  
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
  
## <a name="see-also"></a>Consulte também  
[Funções e exibições de gerenciamento dinâmico &#40; relacionadas à execução Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
[sys.DM exec_sql_text &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
[sys.DM exec_query_plan &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)    
[sys.DM exec_query_stats &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)    
[exec_trigger_stats &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)    
[exec_cached_plans &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)    
  
  


