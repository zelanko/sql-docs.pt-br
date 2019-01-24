---
title: sys.query_store_query (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 397f7d5317fd5033f735b938f7d2f11ec80417bc
ms.sourcegitcommit: 3d50caa30681bf384f5628b1dd3e06e24fc910cd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54838083"
---
# <a name="sysquerystorequery-transact-sql"></a>sys.query_store_query (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Contém informações sobre a consulta e suas estatísticas de execução geral agregado tempo de execução associado.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**query_id**|**bigint**|Chave primária.|  
|**query_text_id**|**bigint**|Chave estrangeira. Joins to [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)|  
|**context_settings_id**|**bigint**|Chave estrangeira. Joins to [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|  
|**object_id**|**bigint**|ID do objeto de banco de dados que a consulta faz parte do (procedimento armazenado, gatilho, UDF do CLR/UDAgg, etc.). 0 se a consulta não é executada como parte de um objeto de banco de dados (consultas ad hoc).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|  
|**batch_sql_handle**|**varbinary(64)**|ID do lote de instrução de consulta faz parte. Populado somente se a consulta faz referência a tabelas temporárias ou variáveis de tabela.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará *nulo*.|  
|**query_hash**|**binary(8)**|Hash MD5 da consulta individual, com base na árvore de lógica de consulta. Inclui dicas do otimizador.|  
|**is_internal_query**|**bit**|A consulta foi gerada internamente.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|  
|**query_parameterization_type**|**tinyint**|Tipo de parametrização:<br /><br /> 0 – none<br /><br /> 1 - usuário<br /><br /> 2 - simples<br /><br /> 3 - forçada<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|  
|**query_parameterization_type_desc**|**nvarchar(60)**|Descrição textual para o tipo de parametrização.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará *None*.|  
|**initial_compile_start_time**|**datetimeoffset**|Iniciar tempo de compilação.|  
|**last_compile_start_time**|**datetimeoffset**|Iniciar tempo de compilação.|  
|**last_execution_time**|**datetimeoffset**|Último tempo de execução refere-se para a última hora de término do/plano de consulta.|  
|**last_compile_batch_sql_handle**|**varbinary(64)**|Identificador do último lote SQL em que a consulta foi usada última vez. Ele pode ser fornecido como entrada para [DM exec_sql_text &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md) para obter o texto completo do lote.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará *nulo*.|  
|**last_compile_batch_offset_start**|**bigint**|Informações que podem ser fornecidas para DM exec_sql_text, juntamente com last_compile_batch_sql_handle.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_compile_batch_offset_end**|**bigint**|Informações que podem ser fornecidas para DM exec_sql_text, juntamente com last_compile_batch_sql_handle.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|  
|**count_compiles**|**bigint**|Estatísticas de compilação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará um (1).|  
|**avg_compile_duration**|**float**|Estatísticas de compilação em microssegundos.|  
|**last_compile_duration**|**bigint**|Estatísticas de compilação em microssegundos.|  
|**avg_bind_duration**|**float**|Estatísticas de associação em microssegundos.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|  
|**last_bind_duration**|**bigint**|Estatísticas de associação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|  
|**avg_bind_cpu_time**|**float**|Estatísticas de associação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|  
|**last_bind_cpu_time**|**bigint**|Estatísticas de associação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|  
|**avg_optimize_duration**|**float**|Estatísticas de otimização em microssegundos.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_optimize_duration**|**bigint**|Estatísticas de otimização.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**avg_optimize_cpu_time**|**float**|Estatísticas de otimização em microssegundos.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_optimize_cpu_time**|**bigint**|Estatísticas de otimização.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**avg_compile_memory_kb**|**float**|Compile estatísticas de memória.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_compile_memory_kb**|**bigint**|Compile estatísticas de memória.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_compile_memory_kb**|**bigint**|Compile estatísticas de memória.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**is_clouddb_internal_query**|**bit**|Sempre 0 no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no local.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
  
## <a name="permissions"></a>Permissões  
 Requer o **VIEW DATABASE STATE** permissão.  
  
## <a name="see-also"></a>Consulte também  
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Procedimentos armazenados do Repositório de Consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
