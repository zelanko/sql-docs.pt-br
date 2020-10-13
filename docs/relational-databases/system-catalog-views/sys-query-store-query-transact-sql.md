---
description: sys.query_store_query (Transact-SQL)
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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1099243569f74cc5c50c90de1ec7bf35a5c53d51
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "92005813"
---
# <a name="sysquery_store_query-transact-sql"></a>sys.query_store_query (Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  Contém informações sobre a consulta e suas estatísticas de execução de tempo de execução agregadas em geral associadas.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**query_id**|**bigint**|Chave primária.|  
|**query_text_id**|**bigint**|Chave estrangeira. Junções para [sys.query_store_query_text &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)|  
|**context_settings_id**|**bigint**|Chave estrangeira. Junções para [sys.query_context_settings &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md).<br/>**Observação:** A análise de Synapse do Azure sempre retornará zero (0).|  
|**object_id**|**bigint**|ID do objeto de banco de dados do qual a consulta faz parte (procedimento armazenado, gatilho, UDF/UDAgg CLR, etc.). 0 se a consulta não for executada como parte de um objeto de banco de dados (consulta ad-hoc).<br/>**Observação:** A análise de Synapse do Azure sempre retornará zero (0).|  
|**batch_sql_handle**|**varbinary(64)**|ID do lote de instruções do qual a consulta faz parte. Populado somente se a consulta fizer referência a tabelas temporárias ou variáveis de tabela.<br/>**Observação:** A análise de Synapse do Azure sempre retornará *NULL*.|  
|**query_hash**|**binário (8)**|Hash MD5 da consulta individual, com base na árvore de consulta lógica. Inclui dicas do otimizador.|  
|**is_internal_query**|**bit**|A consulta foi gerada internamente.<br/>**Observação:** A análise de Synapse do Azure sempre retornará zero (0).|  
|**query_parameterization_type**|**tinyint**|Tipo de parametrização:<br /><br /> 0 – Nenhum<br /><br /> 1-usuário<br /><br /> 2 – simples<br /><br /> 3-forçado<br/>**Observação:** A análise de Synapse do Azure sempre retornará zero (0).|  
|**query_parameterization_type_desc**|**nvarchar(60)**|Descrição textual para o tipo de parametrização.<br/>**Observação:** O Azure Synapse Analytics sempre retornará *nenhum*.|  
|**initial_compile_start_time**|**datetimeoffset**|Hora de início da compilação.|  
|**last_compile_start_time**|**datetimeoffset**|Hora de início da compilação.|  
|**last_execution_time**|**datetimeoffset**|A hora da última execução refere-se à última hora de término da consulta/plano.|  
|**last_compile_batch_sql_handle**|**varbinary(64)**|Identificador do último lote SQL no qual a consulta foi usada pela última vez. Ele pode ser fornecido como entrada para [sys.dm_exec_sql_text &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md) para obter o texto completo do lote.<br/>**Observação:** A análise de Synapse do Azure sempre retornará *NULL*.|  
|**last_compile_batch_offset_start**|**bigint**|Informações que podem ser fornecidas para sys.dm_exec_sql_text junto com last_compile_batch_sql_handle.<br/>**Observação:** A análise de Synapse do Azure sempre retornará zero (0).|
|**last_compile_batch_offset_end**|**bigint**|Informações que podem ser fornecidas para sys.dm_exec_sql_text junto com last_compile_batch_sql_handle.<br/>**Observação:** A análise de Synapse do Azure sempre retornará zero (0).|  
|**count_compiles**|**bigint**|Estatísticas de compilação.<br/>**Observação:** A análise de Synapse do Azure sempre retornará um (1).|  
|**avg_compile_duration**|**flutuante**|Estatísticas de compilação em microssegundos.|  
|**last_compile_duration**|**bigint**|Estatísticas de compilação em microssegundos.|  
|**avg_bind_duration**|**flutuante**|Estatísticas de associação em microssegundos.<br/>**Observação:** A análise de Synapse do Azure sempre retornará zero (0).|  
|**last_bind_duration**|**bigint**|Estatísticas de associação.<br/>**Observação:** A análise de Synapse do Azure sempre retornará zero (0).|  
|**avg_bind_cpu_time**|**flutuante**|Estatísticas de associação.<br/>**Observação:** A análise de Synapse do Azure sempre retornará zero (0).|  
|**last_bind_cpu_time**|**bigint**|Estatísticas de associação.<br/>**Observação:** A análise de Synapse do Azure sempre retornará zero (0).|  
|**avg_optimize_duration**|**flutuante**|Estatísticas de otimização em microssegundos.<br/>**Observação:** A análise de Synapse do Azure sempre retornará zero (0).|
|**last_optimize_duration**|**bigint**|Estatísticas de otimização.<br/>**Observação:** A análise de Synapse do Azure sempre retornará zero (0).|
|**avg_optimize_cpu_time**|**flutuante**|Estatísticas de otimização em microssegundos.<br/>**Observação:** A análise de Synapse do Azure sempre retornará zero (0).|
|**last_optimize_cpu_time**|**bigint**|Estatísticas de otimização.<br/>**Observação:** A análise de Synapse do Azure sempre retornará zero (0).|
|**avg_compile_memory_kb**|**flutuante**|Compilar estatísticas de memória.<br/>**Observação:** A análise de Synapse do Azure sempre retornará zero (0).|
|**last_compile_memory_kb**|**bigint**|Compilar estatísticas de memória.<br/>**Observação:** A análise de Synapse do Azure sempre retornará zero (0).|
|**max_compile_memory_kb**|**bigint**|Compilar estatísticas de memória.<br/>**Observação:** A análise de Synapse do Azure sempre retornará zero (0).|
|**is_clouddb_internal_query**|**bit**|Sempre 0 no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] local.<br/>**Observação:** A análise de Synapse do Azure sempre retornará zero (0).|
  
## <a name="permissions"></a>Permissões  
 Requer a permissão **View Database State** .  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sys.database_query_store_options ](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.query_context_settings ](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.query_store_plan ](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.query_store_query_text ](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [&#41;&#40;Transact-SQL de sys.query_store_runtime_stats ](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.query_store_runtime_stats_interval ](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Procedimentos armazenados do Repositório de Consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
