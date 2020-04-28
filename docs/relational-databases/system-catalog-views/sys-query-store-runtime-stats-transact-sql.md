---
title: sys. query_store_runtime_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2019
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
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0bd7f1870a88ae2050445050565e0f268f4d9b0e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "70148290"
---
# <a name="sysquery_store_runtime_stats-transact-sql"></a>sys. query_store_runtime_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Contém informações sobre as informações de estatísticas de execução de tempo de execução da consulta.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**runtime_stats_id**|**bigint**|Identificador da linha que representa as estatísticas de execução de tempo de execução para o **plan_id**, **execution_type** e **runtime_stats_interval_id**. Ele só é exclusivo para os intervalos de estatísticas de tempo de execução anteriores. Para o intervalo ativo no momento, pode haver várias linhas representando estatísticas de tempo de execução para o plano referenciado por **plan_id**, com o tipo de execução representado por **execution_type**. Normalmente, uma linha representa as estatísticas de tempo de execução que são liberadas para o disco, enquanto outras (s) representam o estado na memória. Portanto, para obter o estado real de cada intervalo, você precisa agregar métricas, agrupamento por **plan_id**, **execution_type** e **runtime_stats_interval_id**.<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**plan_id**|**bigint**|Chave estrangeira. Junções em [Sys. query_store_plan &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md).|  
|**runtime_stats_interval_id**|**bigint**|Chave estrangeira. Junções em [Sys. query_store_runtime_stats_interval &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md).|  
|**execution_type**|**tinyint**|Determina o tipo de execução da consulta:<br /><br /> 0-execução regular (concluída com êxito)<br /><br /> 3-execução abortada do cliente iniciada<br /><br /> 4-execução anulada de exceção|  
|**execution_type_desc**|**nvarchar(128)**|Descrição textual do campo de tipo de execução:<br /><br /> 0-regular<br /><br /> 3-anulado<br /><br /> 4-exceção|  
|**first_execution_time**|**datetimeoffset**|Primeiro tempo de execução para o plano de consulta dentro do intervalo de agregação. Isso se refere à hora de término da execução da consulta.|  
|**last_execution_time**|**datetimeoffset**|Hora da última execução do plano de consulta dentro do intervalo de agregação. Isso se refere à hora de término da execução da consulta.|  
|**count_executions**|**bigint**|Contagem total de execuções para o plano de consulta dentro do intervalo de agregação.|  
|**avg_duration**|**float**|Duração média do plano de consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**last_duration**|**bigint**|Última duração do plano de consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**min_duration**|**bigint**|Duração mínima do plano de consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**max_duration**|**bigint**|Duração máxima do plano de consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**stdev_duration**|**float**|Desvio padrão de duração do plano de consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**avg_cpu_time**|**float**|Tempo médio de CPU para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_cpu_time**|**bigint**|Último tempo de CPU para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_cpu_time**|**bigint**|Tempo mínimo de CPU para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_cpu_time**|**bigint**|Tempo máximo de CPU para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**stdev_cpu_time**|**float**|Desvio padrão de tempo de CPU para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**avg_logical_io_reads**|**float**|Número médio de leituras lógicas de e/s para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8 KB de leitura).<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_logical_io_reads**|**bigint**|Último número de leituras lógicas de e/s para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8 KB de leitura).<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_logical_io_reads**|**bigint**|Número mínimo de leituras lógicas de e/s para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8 KB de leitura).<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_logical_io_reads**|**bigint**|Número máximo de leituras lógicas de e/s para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8 KB de leitura).<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**stdev_logical_io_reads**|**float**|O número de e/s lógicas lê o desvio padrão do plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8 KB de leitura).<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**avg_logical_io_writes**|**float**|Número médio de gravações de e/s lógicas para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_logical_io_writes**|**bigint**|Último número de gravações de e/s lógicas para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_logical_io_writes**|**bigint**|Número mínimo de gravações de e/s lógicas para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_logical_io_writes**|**bigint**|Número máximo de gravações de e/s lógicas para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**stdev_logical_io_writes**|**float**|Número de gravações de e/s lógicas padrão para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**avg_physical_io_reads**|**float**|Número médio de leituras de e/s físicas para o plano de consulta dentro do intervalo de agregação (expresso como um número de páginas de 8 KB de leitura).<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_physical_io_reads**|**bigint**|Último número de leituras de e/s físicas para o plano de consulta dentro do intervalo de agregação (expresso como um número de páginas de 8 KB de leitura).<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_physical_io_reads**|**bigint**|Número mínimo de leituras de e/s físicas para o plano de consulta dentro do intervalo de agregação (expresso como um número de páginas de 8 KB de leitura).<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_physical_io_reads**|**bigint**|Número máximo de leituras de e/s físicas para o plano de consulta dentro do intervalo de agregação (expresso como um número de páginas de 8 KB de leitura).<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**stdev_physical_io_reads**|**float**|Número de e/s física lê o desvio padrão do plano de consulta dentro do intervalo de agregação (expresso como um número de páginas de 8 KB de leitura).<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**avg_clr_time**|**float**|Tempo médio de CLR para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_clr_time**|**bigint**|Hora do último CLR para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_clr_time**|**bigint**|Tempo mínimo CLR para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_clr_time**|**bigint**|Tempo máximo de CLR para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**stdev_clr_time**|**float**|Desvio padrão de tempo CLR para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**avg_dop**|**float**|DOP médio (grau de paralelismo) para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_dop**|**bigint**|Último DOP (grau de paralelismo) para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_dop**|**bigint**|DOP mínimo (grau de paralelismo) para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_dop**|**bigint**|DOP máximo (grau de paralelismo) para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**stdev_dop**|**float**|Desvio padrão de DOP (grau de paralelismo) para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**avg_query_max_used_memory**|**float**|Concessão de memória média (relatada como o número de páginas de 8 KB) para o plano de consulta dentro do intervalo de agregação. Sempre 0 para consultas que usam procedimentos com otimização de memória compilados nativamente.<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_query_max_used_memory**|**bigint**|Última concessão de memória (relatada como o número de páginas de 8 KB) para o plano de consulta dentro do intervalo de agregação. Sempre 0 para consultas que usam procedimentos com otimização de memória compilados nativamente.<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_query_max_used_memory**|**bigint**|Concessão mínima de memória (relatada como o número de páginas de 8 KB) para o plano de consulta dentro do intervalo de agregação. Sempre 0 para consultas que usam procedimentos com otimização de memória compilados nativamente.<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_query_max_used_memory**|**bigint**|Concessão máxima de memória (relatada como o número de páginas de 8 KB) para o plano de consulta dentro do intervalo de agregação. Sempre 0 para consultas que usam procedimentos com otimização de memória compilados nativamente.<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**stdev_query_max_used_memory**|**float**|Desvio padrão de concessão de memória (relatado como o número de páginas de 8 KB) para o plano de consulta dentro do intervalo de agregação. Sempre 0 para consultas que usam procedimentos com otimização de memória compilados nativamente.<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**avg_rowcount**|**float**|Número médio de linhas retornadas para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_rowcount**|**bigint**|Número de linhas retornadas pela última execução do plano de consulta dentro do intervalo de agregação.<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_rowcount**|**bigint**|Número mínimo de linhas retornadas para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_rowcount**|**bigint**|Número máximo de linhas retornadas para o plano de consulta dentro do intervalo de agregação.|  
|**stdev_rowcount**|**float**|Número de desvio padrão de linhas retornadas para o plano de consulta dentro do intervalo de agregação.|
|**avg_log_bytes_used**|**float**|Número médio de bytes no log de banco de dados usados pelo plano de consulta, dentro do intervalo de agregação.<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_log_bytes_used**|**bigint**|Número de bytes no log de banco de dados usados pela última execução do plano de consulta, dentro do intervalo de agregação.<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_log_bytes_used**|**bigint**|Número mínimo de bytes no log de banco de dados usado pelo plano de consulta, dentro do intervalo de agregação.<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_log_bytes_used**|**bigint**|Número máximo de bytes no log de banco de dados usado pelo plano de consulta, dentro do intervalo de agregação.<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|
|**stdev_log_bytes_used**|**float**|Desvio padrão do número de bytes no log de banco de dados usado por um plano de consulta, dentro do intervalo de agregação.<br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|  
|**avg_tempdb_space_used**|**float**|Número médio de leituras de página para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8 KB de leitura).<br><br/>**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]começando com [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]) e.|
|**last_tempdb_space_used**|**bigint**|Último número de leituras de página para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8 KB de leitura).<br><br/>**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]começando com [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]) e.|
|**min_tempdb_space_used**|**bigint**|Número mínimo de leituras de página para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8 KB de leitura).<br><br/>**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]começando com [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]) e.|
|**max_tempdb_space_used**|**bigint**|Número máximo de leituras de página para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8 KB de leitura).<br><br/>**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]começando com [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]) e.|
|**stdev_tempdb_space_used**|**float**|Número de leituras de página desvio padrão do plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8 KB de leitura).<br><br/>**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]começando com [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]) e.|
|**avg_page_server_io_reads**|**float**|Número médio de leituras de e/s de servidor de página para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8 KB de leitura).<br><br/>**Aplica-se a:** Hiperescala do banco de dados SQL do Azure</br>**Observação:** O Azure SQL Data Warehouse, o banco de BD SQL do Azure, MI (não hiperescala) sempre retornará zero (0).|
|**last_page_server_io_reads**|**bigint**|Último número de leituras de e/s de servidor de página para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8 KB de leitura).<br><br/>**Aplica-se a:** Hiperescala do banco de dados SQL do Azure</br>**Observação:** O Azure SQL Data Warehouse, o banco de BD SQL do Azure, MI (não hiperescala) sempre retornará zero (0).|
|**min_page_server_io_reads**|**bigint**|Número mínimo de leituras de e/s de servidor de página para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8 KB de leitura).<br><br/>**Aplica-se a:** Hiperescala do banco de dados SQL do Azure</br>**Observação:** O Azure SQL Data Warehouse, o banco de BD SQL do Azure, MI (não hiperescala) sempre retornará zero (0).|
|**max_page_server_io_reads**|**bigint**|Número máximo de leituras de e/s de servidor de página para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8 KB de leitura).<br><br/>**Aplica-se a:** Hiperescala do banco de dados SQL do Azure</br>**Observação:** O Azure SQL Data Warehouse, o banco de BD SQL do Azure, MI (não hiperescala) sempre retornará zero (0).|
|**stdev_page_server_io_reads**|**float**|Número de e/s de servidor de páginas lê desvio padrão para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8 KB de leitura).<br><br/>**Aplica-se a:** Hiperescala do banco de dados SQL do Azure</br>**Observação:** O Azure SQL Data Warehouse, o banco de BD SQL do Azure, MI (não hiperescala) sempre retornará zero (0).|
  
## <a name="permissions"></a>Permissões  
Requer a permissão `VIEW DATABASE STATE`.  
  
## <a name="see-also"></a>Consulte Também  
 [sys. database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys. query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys. query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys. query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys. query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys. query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitorando o desempenho usando o Repositório de Consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Repositório de Consultas procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)    
 [Melhor prática com o Repositório de Consultas](../../relational-databases/performance/best-practice-with-the-query-store.md)   
  
