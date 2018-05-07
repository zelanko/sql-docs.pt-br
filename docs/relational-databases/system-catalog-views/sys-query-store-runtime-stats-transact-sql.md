---
title: query_store_runtime_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SYS.QUERY_STORE_RUNTIME_STATS_TSQL
- QUERY_STORE_RUNTIME_STATS_TSQL
- SYS.QUERY_STORE_RUNTIME_STATS
- QUERY_STORE_RUNTIME_STATS
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_runtime_stats catalog view
- sys.query_store_runtime_stats catalog view
ms.assetid: ccf7a57c-314b-450c-bd34-70749a02784a
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 85bb7aa5bf91f8d357556adac9e58fb6ab83df24
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sysquerystoreruntimestats-transact-sql"></a>query_store_runtime_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Contém informações sobre as informações de estatísticas de execução de tempo de execução da consulta.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**runtime_stats_id**|**bigint**|Identificador da linha que representa as estatísticas de execução de tempo para o **plan_id**, **execution_type** e **runtime_stats_interval_id**. É exclusivo somente para os últimos intervalos de estatísticas de tempo de execução. Para o intervalo ativo no momento pode haver várias linhas que representa as estatísticas de tempo de execução para o plano referenciada por **plan_id**, com o tipo de execução representado por **execution_type**. Normalmente, uma linha representa as estatísticas de tempo de execução são liberadas para disco, enquanto outros (s) representam o estado na memória. Portanto, para obter o estado real para cada intervalo precisar métricas agregadas, agrupando **plan_id**, **execution_type** e **runtime_stats_interval_id**. |  
|**plan_id**|**bigint**|Chave estrangeira. Une a [query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md).|  
|**runtime_stats_interval_id**|**bigint**|Chave estrangeira. Une a [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md).|  
|**execution_type**|**tinyint**|Determina o tipo de execução de consulta:<br /><br /> 0 – execução regular (concluída com êxito)<br /><br /> 3 – cliente iniciado anulou a execução<br /><br /> 4 - exceção anulou a execução|  
|**execution_type_desc**|**nvarchar(128)**|Descrição textual do campo de tipo de execução:<br /><br /> 0 – regular<br /><br /> 3 – anulada<br /><br /> 4 - exceção|  
|**first_execution_time**|**datetimeoffset**|Tempo de execução primeiro para o plano de consulta dentro do intervalo de agregação.|  
|**last_execution_time**|**datetimeoffset**|Horário da última execução da consulta de plano no intervalo de agregação.|  
|**count_executions**|**bigint**|Contagem total de execuções do plano de consulta dentro do intervalo de agregação.|  
|**avg_duration**|**float**|Média de duração para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**last_duration**|**bigint**|Última duração para a consulta de plano no intervalo de agregação (relatado em microssegundos).|  
|**min_duration**|**bigint**|Duração mínima para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**max_duration**|**bigint**|Duração máxima para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**stdev_duration**|**float**|Desvio padrão de duração para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**avg_cpu_time**|**float**|Tempo médio de CPU para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**last_cpu_time**|**bigint**|Último tempo de CPU para a consulta de plano no intervalo de agregação (relatado em microssegundos).|  
|**min_cpu_time**|**bigint**|Tempo mínimo de CPU para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**max_cpu_time**|**bigint**|Tempo máximo de CPU para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**stdev_cpu_time**|**float**|Desvio de padrão de tempo de CPU para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**avg_logical_io_reads**|**float**|Número médio de e/s lógica lê do plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8KB de leitura).|  
|**last_logical_io_reads**|**bigint**|Último número de e/s lógica lê do plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8KB de leitura).|  
|**min_logical_io_reads**|**bigint**|Lê o número mínimo de e/s lógica para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8KB de leitura).|  
|**max_logical_io_reads**|**bigint**|Lê o número máximo de e/s lógica para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8KB de leitura). |  
|**stdev_logical_io_reads**|**float**|Número de e/s lógica lê o desvio padrão para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8KB de leitura).|  
|**avg_logical_io_writes**|**float**|Número médio de e/s lógica grava para o plano de consulta dentro do intervalo de agregação.|  
|**last_logical_io_writes**|**bigint**|Último número de e/s lógica grava para o plano de consulta dentro do intervalo de agregação.|  
|**min_logical_io_writes**|**bigint**|Número mínimo de e/s lógica grava para o plano de consulta dentro do intervalo de agregação.|  
|**max_logical_io_writes**|**bigint**|Número máximo de e/s lógica grava para o plano de consulta dentro do intervalo de agregação.|  
|**stdev_logical_io_writes**|**float**|Número de e/s lógica grava o desvio padrão para o plano de consulta dentro do intervalo de agregação.|  
|**avg_physical_io_reads**|**float**|Número médio de e/s física lê do plano de consulta dentro do intervalo de agregação (expressado como um número de páginas de 8KB de leitura).|  
|**last_physical_io_reads**|**bigint**|Último número de e/s física lê do plano de consulta dentro do intervalo de agregação (expressado como um número de páginas de 8KB de leitura).|  
|**min_physical_io_reads**|**bigint**|Lê o número mínimo de e/s física para o plano de consulta dentro do intervalo de agregação (expressado como um número de páginas de 8KB de leitura).|  
|**max_physical_io_reads**|**bigint**|Lê o número máximo de e/s física para o plano de consulta dentro do intervalo de agregação (expressado como um número de páginas de 8KB de leitura).|  
|**stdev_physical_io_reads**|**float**|Número de e/s física lê o desvio padrão para o plano de consulta dentro do intervalo de agregação (expressado como um número de páginas de 8KB de leitura).|  
|**avg_clr_time**|**float**|Tempo médio de CLR para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**last_clr_time**|**bigint**|Planejar a última hora do CLR para a consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**min_clr_time**|**bigint**|Tempo mínimo de CLR para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**max_clr_time**|**bigint**|Tempo máximo de CLR para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**stdev_clr_time**|**float**|Desvio do padrão de tempo do CLR para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**avg_dop**|**float**|Médio DOP (grau de paralelismo) para o plano de consulta dentro do intervalo de agregação.|  
|**last_dop**|**bigint**|Última DOP (grau de paralelismo) para o plano de consulta dentro do intervalo de agregação.|  
|**min_dop**|**bigint**|Mínimo DOP (grau de paralelismo) para o plano de consulta dentro do intervalo de agregação.|  
|**max_dop**|**bigint**|Máximo DOP (grau de paralelismo) para o plano de consulta dentro do intervalo de agregação.|  
|**stdev_dop**|**float**|Desvio padrão DOP (grau de paralelismo) para o plano de consulta dentro do intervalo de agregação.|  
|**avg_query_max_used_memory**|**float**|Médio concessão de memória (relatado como o número de páginas de 8 KB) para o plano de consulta dentro do intervalo de agregação. Sempre 0 para consultas que usam nativamente compilada procedimentos de otimização de memória.|  
|**last_query_max_used_memory**|**bigint**|Última concessão de memória (relatado como o número de páginas de 8 KB) para o plano de consulta dentro do intervalo de agregação. Sempre 0 para consultas que usam nativamente compilada procedimentos de otimização de memória.|  
|**min_query_max_used_memory**|**bigint**|Concessão de memória mínima (relatado como o número de páginas de 8 KB) para o plano de consulta dentro do intervalo de agregação. Sempre 0 para consultas que usam nativamente compilada procedimentos de otimização de memória.|  
|**max_query_max_used_memory**|**bigint**|Concessão máxima de memória (relatado como o número de páginas de 8 KB) para o plano de consulta dentro do intervalo de agregação. Sempre 0 para consultas que usam nativamente compilada procedimentos de otimização de memória.|  
|**stdev_query_max_used_memory**|**float**|Desvio padrão (relatado como o número de páginas de 8 KB) de concessão de memória para o plano de consulta dentro do intervalo de agregação. Sempre 0 para consultas que usam nativamente compilada procedimentos de otimização de memória.|  
|**avg_rowcount**|**float**|Número médio de linhas retornadas para o plano de consulta dentro do intervalo de agregação.|  
|**last_rowcount**|**bigint**|Número de linhas retornadas pela última execução do plano de consulta dentro do intervalo de agregação.|  
|**min_rowcount**|**bigint**|Planejar o número mínimo de linhas retornadas para a consulta dentro do intervalo de agregação.|  
|**max_rowcount**|**bigint**|Planejar o número máximo de linhas retornadas para a consulta dentro do intervalo de agregação.|  
|**stdev_rowcount**|**float**|Número de desvio padrão de linhas retornadas para o plano de consulta dentro do intervalo de agregação.|
|**avg_log_bytes_used**|**float**|Número médio de bytes no log do banco de dados usado pelo plano de consulta dentro do intervalo de agregação. Aplica-se **somente para o banco de dados SQL do Azure**.|    
|**last_log_bytes_used**|**bigint**|Número de bytes no log do banco de dados usado pela última execução do plano de consulta dentro do intervalo de agregação. Aplica-se **somente para o banco de dados SQL do Azure**.|  
|**min_log_bytes_used**|**bigint**|Número mínimo de bytes no log do banco de dados usado pelo plano de consulta dentro do intervalo de agregação.  Aplica-se **somente para o banco de dados SQL do Azure**.|  
|**max_log_bytes_used**|**bigint**|Número máximo de bytes no log do banco de dados usado pelo plano de consulta dentro do intervalo de agregação.  Aplica-se **somente para o banco de dados SQL do Azure**.| 
|**stdev_log_bytes_used**|**float**|Desvio padrão do número de bytes no log do banco de dados usado por um plano de consulta dentro do intervalo de agregação.  Aplica-se **somente para o banco de dados SQL do Azure**.|
  
## <a name="permissions"></a>Permissões  
 Requer o **VIEW DATABASE STATE** permissão.  
  
## <a name="see-also"></a>Consulte também  
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Procedimentos armazenados do repositório de consulta &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
