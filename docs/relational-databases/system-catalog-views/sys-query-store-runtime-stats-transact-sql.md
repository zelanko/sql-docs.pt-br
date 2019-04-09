---
title: sys.query_store_runtime_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3392bcde00439981a401c908ca7a1898d9d026f5
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59242304"
---
# <a name="sysquerystoreruntimestats-transact-sql"></a>sys.query_store_runtime_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Contém informações sobre as informações de estatísticas de execução de tempo de execução da consulta.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**runtime_stats_id**|**BIGINT**|Identificador da linha que representa as estatísticas de execução de tempo de execução para o **plan_id**, **execution_type** e **runtime_stats_interval_id**. Ele é exclusivo somente para os intervalos de estatísticas de tempo de execução anterior. Para o intervalo ativo no momento pode haver várias linhas que representa as estatísticas de tempo de execução para o plano referenciado pelo **plan_id**, com o tipo de execução representado pelo **execution_type**. Normalmente, uma linha representa as estatísticas de tempo de execução que são liberadas no disco, enquanto outras (s) representam o estado na memória. Portanto, para obter o estado real para cada intervalo é necessário agregar as métricas, agrupando **plan_id**, **execution_type** e **runtime_stats_interval_id**.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**plan_id**|**BIGINT**|Chave estrangeira. Ingressa [query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md).|  
|**runtime_stats_interval_id**|**BIGINT**|Chave estrangeira. Ingressa [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md).|  
|**execution_type**|**TINYINT**|Determina o tipo de execução da consulta:<br /><br /> 0 - execução regular (concluída com êxito)<br /><br /> 3 - cliente iniciado anulou a execução<br /><br /> 4 - exceção anulou a execução|  
|**execution_type_desc**|**nvarchar(128)**|Descrição textual do campo de tipo de execução:<br /><br /> 0 - regular<br /><br /> 3 - anulada<br /><br /> 4 - exceção|  
|**first_execution_time**|**datetimeoffset**|Primeiro tempo de execução para o plano de consulta dentro do intervalo de agregação.|  
|**last_execution_time**|**datetimeoffset**|Último tempo de execução para a consulta planejar dentro do intervalo de agregação.|  
|**count_executions**|**BIGINT**|Contagem total de execuções do plano de consulta dentro do intervalo de agregação.|  
|**avg_duration**|**FLOAT**|Média de duração para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**last_duration**|**BIGINT**|Duração da consulta do último plano dentro do intervalo de agregação (relatado em microssegundos).|  
|**min_duration**|**BIGINT**|Duração mínima para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**max_duration**|**BIGINT**|Duração máxima para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**stdev_duration**|**FLOAT**|Desvio padrão de duração para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**avg_cpu_time**|**FLOAT**|Tempo médio de CPU para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_cpu_time**|**BIGINT**|Último tempo de CPU para a consulta planejar dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_cpu_time**|**BIGINT**|Tempo mínimo de CPU para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_cpu_time**|**BIGINT**|Tempo máximo de CPU para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**stdev_cpu_time**|**FLOAT**|Desvio de padrão de tempo de CPU para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**avg_logical_io_reads**|**FLOAT**|Lê o número médio de e/s lógica para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8KB de leitura).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_logical_io_reads**|**BIGINT**|Último número de e/s lógicas lê para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8KB de leitura).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_logical_io_reads**|**BIGINT**|Lê o número mínimo de e/s lógica para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8KB de leitura).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_logical_io_reads**|**BIGINT**|Lê o número máximo de e/s lógica para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8KB de leitura).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**stdev_logical_io_reads**|**FLOAT**|Número de e/s lógicas lê o desvio padrão para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8KB de leitura).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**avg_logical_io_writes**|**FLOAT**|Número médio de e/s lógicas grava para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_logical_io_writes**|**BIGINT**|Último número de e/s lógicas grava para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_logical_io_writes**|**BIGINT**|Número mínimo de e/s lógicas grava para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_logical_io_writes**|**BIGINT**|Número máximo de e/s lógicas grava para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**stdev_logical_io_writes**|**FLOAT**|Número de e/s lógicas grava o desvio padrão para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**avg_physical_io_reads**|**FLOAT**|Lê o número médio de e/s física para o plano de consulta dentro do intervalo de agregação (expressado como um número de páginas de 8KB de leitura).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_physical_io_reads**|**BIGINT**|Último número de e/s física lê para o plano de consulta dentro do intervalo de agregação (expressado como um número de páginas de 8KB de leitura).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_physical_io_reads**|**BIGINT**|Lê o número mínimo de e/s física para o plano de consulta dentro do intervalo de agregação (expressado como um número de páginas de 8KB de leitura).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_physical_io_reads**|**BIGINT**|Lê o número máximo de e/s física para o plano de consulta dentro do intervalo de agregação (expressado como um número de páginas de 8KB de leitura).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**stdev_physical_io_reads**|**FLOAT**|Número de e/s física lê o desvio padrão para o plano de consulta dentro do intervalo de agregação (expressado como um número de páginas de 8KB de leitura).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**avg_clr_time**|**FLOAT**|Tempo médio de CLR para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_clr_time**|**BIGINT**|Última hora CLR para a consulta planejar dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_clr_time**|**BIGINT**|Tempo mínimo de CLR para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_clr_time**|**BIGINT**|Tempo máximo de CLR para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**stdev_clr_time**|**FLOAT**|Desvio do padrão de tempo do CLR para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**avg_dop**|**FLOAT**|Média DOP (grau de paralelismo) para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_dop**|**BIGINT**|Último DOP (grau de paralelismo) para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_dop**|**BIGINT**|Mínimo DOP (grau de paralelismo) para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_dop**|**BIGINT**|Máximo DOP (grau de paralelismo) para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**stdev_dop**|**FLOAT**|Desvio padrão DOP (grau de paralelismo) para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**avg_query_max_used_memory**|**FLOAT**|Concessão de memória média (relatado como o número de páginas de 8 KB) para o plano de consulta dentro do intervalo de agregação. Sempre 0 para consultas que usam nativamente compilado procedimentos com otimização de memória.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_query_max_used_memory**|**BIGINT**|Última concessão de memória (relatado como o número de páginas de 8 KB) para o plano de consulta dentro do intervalo de agregação. Sempre 0 para consultas que usam nativamente compilado procedimentos com otimização de memória.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_query_max_used_memory**|**BIGINT**|Concessão de memória mínima (relatado como o número de páginas de 8 KB) para o plano de consulta dentro do intervalo de agregação. Sempre 0 para consultas que usam nativamente compilado procedimentos com otimização de memória.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_query_max_used_memory**|**BIGINT**|Concessão máxima de memória (relatado como o número de páginas de 8 KB) para o plano de consulta dentro do intervalo de agregação. Sempre 0 para consultas que usam nativamente compilado procedimentos com otimização de memória.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**stdev_query_max_used_memory**|**FLOAT**|Desvio padrão (relatado como o número de páginas de 8 KB) de concessão de memória para o plano de consulta dentro do intervalo de agregação. Sempre 0 para consultas que usam nativamente compilado procedimentos com otimização de memória.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**avg_rowcount**|**FLOAT**|Número médio de linhas retornadas para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_rowcount**|**BIGINT**|Número de linhas retornadas pela última execução do plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_rowcount**|**BIGINT**|Número mínimo de linhas retornadas para a consulta planejar dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_rowcount**|**BIGINT**|Número máximo de linhas retornadas para a consulta planejar dentro do intervalo de agregação.|  
|**stdev_rowcount**|**FLOAT**|Número de desvio padrão de linhas retornadas para o plano de consulta dentro do intervalo de agregação.|
|**avg_log_bytes_used**|**FLOAT**|Número médio de bytes no log do banco de dados usadas pelo plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_log_bytes_used**|**BIGINT**|Número de bytes no log do banco de dados usado pela última execução do plano de consulta, dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_log_bytes_used**|**BIGINT**|Número mínimo de bytes no log do banco de dados usadas pelo plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_log_bytes_used**|**BIGINT**|Número máximo de bytes no log do banco de dados usadas pelo plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**stdev_log_bytes_used**|**FLOAT**|Desvio padrão do número de bytes no log do banco de dados usado por um plano de consulta, dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
  
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
 [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Procedimentos armazenados do repositório de consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
