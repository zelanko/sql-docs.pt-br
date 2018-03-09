---
title: query_store_query (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/29/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- QUERY_STORE_QUERY
- SYS.QUERY_STORE_QUERY_TSQL
- SYS.QUERY_STORE_QUERY
- QUERY_STORE_QUERY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_query catalog view
- sys.query_store_query catalog view
ms.assetid: bdee149e-7556-4fc3-8242-925dd4b7b6ac
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ef06fab57c78c83e4c38993cf0acdaf60fcc0f39
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sysquerystorequery-transact-sql"></a>query_store_query (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Contém informações sobre a consulta e suas estatísticas de execução de tempo de agregados geral associado.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**query_id**|**bigint**|Chave primária.|  
|**query_text_id**|**bigint**|Chave estrangeira. Une a [query_store_query_text &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)|  
|**context_settings_id**|**bigint**|Chave estrangeira. Une a [sys.query_context_settings &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md).|  
|**object_id**|**bigint**|ID do objeto de banco de dados que a consulta faz parte do (procedimento armazenado, gatilho, o CLR UDF/UDAgg, etc.). 0 se a consulta não é executada como parte de um objeto de banco de dados (consultas ad hoc).|  
|**batch_sql_handle**|**varbinary(64)**|ID do lote de instrução de consulta faz parte. Populado somente se a consulta faz referência a tabelas temporárias ou variáveis de tabela.|  
|**query_hash**|**binary (8)**|Hash MD5 de consulta individual, com base na árvore de lógica de consulta. Inclui dicas de otimização.|  
|**is_internal_query**|**bit**|A consulta foi gerada internamente.|  
|**query_parameterization_type**|**tinyint**|Tipo de parametrização:<br /><br /> 0 – none<br /><br /> 1 – usuário<br /><br /> 2 – simples<br /><br /> 3 – forçado|  
|**query_parameterization_type_desc**|**nvarchar (60)**|Descrição textual para o tipo de parametrização.|  
|**initial_compile_start_time**|**datetimeoffset**|Compile a hora de início.|  
|**last_compile_start_time**|**datetimeoffset**|Compile a hora de início.|  
|**last_execution_time**|**datetimeoffset**|Horário da última execução refere-se para a última hora de término do plano de consulta /.|  
|**last_compile_batch_sql_handle**|**varbinary(64)**|Identificador do último lote SQL no qual consulta foi usada anteriormente. Ele pode ser fornecido como entrada para [dm_exec_sql_text &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md) para obter o texto completo do lote.|  
|**last_compile_batch_offset_start**|**bigint**|Informações que podem ser fornecidas para dm_exec_sql_text juntamente com last_compile_batch_sql_handle.|  
|**last_compile_batch_offset_end**|**bigint**|Informações que podem ser fornecidas para dm_exec_sql_text juntamente com last_compile_batch_sql_handle.|  
|**count_compiles**|**bigint**|Estatísticas de compilação.|  
|**avg_compile_duration**|**float**|Estatísticas de compilação em microssegundos.|  
|**last_compile_duration**|**bigint**|Estatísticas de compilação em microssegundos.|  
|**avg_bind_duration**|**float**|Estatísticas de associação em microssegundos.|  
|**last_bind_duration**|**bigint**|Estatísticas de associação.|  
|**avg_bind_cpu_time**|**float**|Estatísticas de associação.|  
|**last_bind_cpu_time**|**bigint**|Estatísticas de associação.|  
|**avg_optimize_duration**|**float**|Estatísticas de otimização em microssegundos.|  
|**last_optimize_duration**|**bigint**|Estatísticas de otimização.|  
|**avg_optimize_cpu_time**|**float**|Estatísticas de otimização em microssegundos.|  
|**last_optimize_cpu_time**|**bigint**|Estatísticas de otimização.|  
|**avg_compile_memory_kb**|**float**|Compile estatísticas de memória.|  
|**last_compile_memory_kb**|**bigint**|Compile estatísticas de memória.|  
|**max_compile_memory_kb**|**bigint**|Compile estatísticas de memória.|  
|**is_clouddb_internal_query**|**bit**|Sempre 0 em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] local.|  
  
## <a name="permissions"></a>Permissões  
 Requer o **VIEW DATABASE STATE** permissão.  
  
## <a name="see-also"></a>Consulte também  
 [database_query_store_options &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [query_store_plan &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [query_store_query_text &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [query_store_runtime_stats &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_runtime_stats_interval &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Procedimentos armazenados do Repositório de Consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
