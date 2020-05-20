---
title: sys. query_store_wait_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.query_store_wait_stats
- query_store_wait_stats
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_wait_stats catalog view
- sys.query_store_wait_stats catalog view
ms.assetid: ccf7a57c-314b-450c-bd34-70749a02784a
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f3c94f7f23697539b000c9c76dc1d0970a56a96d
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82834083"
---
# <a name="sysquery_store_wait_stats-transact-sql"></a>sys. query_store_wait_stats (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Contém informações sobre as informações de espera da consulta.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**wait_stats_id**|**bigint**|Identificador da linha que representa as estatísticas de espera para o plan_id, runtime_stats_interval_id, execution_type e wait_category. Ele só é exclusivo para os intervalos de estatísticas de tempo de execução anteriores. Para o intervalo ativo no momento, pode haver várias linhas representando estatísticas de espera para o plano referenciado por plan_id, com o tipo de execução representado por execution_type e a categoria de espera representada por wait_category. Normalmente, uma linha representa as estatísticas de espera liberadas para o disco, enquanto outras (s) representam o estado na memória. Portanto, para obter o estado real de cada intervalo, você precisa agregar métricas, agrupamento por plan_id, runtime_stats_interval_id, execution_type e wait_category. |  
|**plan_id**|**bigint**|Chave estrangeira. Junções em [Sys. query_store_plan &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md).|  
|**runtime_stats_interval_id**|**bigint**|Chave estrangeira. Junções em [Sys. query_store_runtime_stats_interval &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md).|  
|**wait_category**|**tinyint**|Os tipos de espera são categorizados usando a tabela abaixo e, em seguida, o tempo de espera é agregado entre essas categorias de espera. Diferentes categorias de espera exigem uma análise de acompanhamento diferente para resolver o problema, mas os tipos de espera da mesma categoria levam a experiências de solução de problemas semelhantes, e fornecer a consulta afetada além das esperas é a peça que falta para concluir a maioria dessas investigações com êxito.|
|**wait_category_desc**|**nvarchar(128)**|Para descrição textual do campo de categoria de espera, examine a tabela a seguir.|
|**execution_type**|**tinyint**|Determina o tipo de execução da consulta:<br /><br /> 0-execução regular (concluída com êxito)<br /><br /> 3-execução abortada do cliente iniciada<br /><br /> 4-execução anulada de exceção|  
|**execution_type_desc**|**nvarchar(128)**|Descrição textual do campo de tipo de execução:<br /><br /> 0-regular<br /><br /> 3-anulado<br /><br /> 4-exceção|  
|**total_query_wait_time_ms**|**bigint**|`CPU wait`Tempo total do plano de consulta dentro do intervalo de agregação e da categoria de espera (relatado em milissegundos).|
|**avg_query_wait_time_ms**|**float**|Duração média de espera do plano de consulta por execução dentro do intervalo de agregação e da categoria de espera (relatada em milissegundos).|
|**last_query_wait_time_ms**|**bigint**|Duração da última espera do plano de consulta dentro do intervalo de agregação e da categoria de espera (relatada em milissegundos).|
|**min_query_wait_time_ms**|**bigint**|`CPU wait`Tempo mínimo para o plano de consulta dentro do intervalo de agregação e a categoria de espera (relatados em milissegundos).|
|**max_query_wait_time_ms**|**bigint**|`CPU wait`Tempo máximo para o plano de consulta dentro do intervalo de agregação e a categoria de espera (relatados em milissegundos).|
|**stdev_query_wait_time_ms**|**float**|`Query wait`desvio padrão da duração do plano de consulta dentro do intervalo de agregação e da categoria de espera (relatado em milissegundos).|

## <a name="wait-categories-mapping-table"></a>Tabela de mapeamento de categorias de espera

"%" é usado como um curinga
  
|Valor inteiro|Categoria de espera|Os tipos de espera incluem na categoria|  
|-----------------|---------------|-----------------|  
|**0**|**Conhecidos**|Unknown |  
|**1**|**CPU**|SOS_SCHEDULER_YIELD|
|**2**|**Thread de trabalho**|THREADPOOL|
|**3**|**Proprietário**|LCK_M_%|
|**4**|**Trava**|LATCH_%|
|**5**|**Trava do buffer**|PAGELATCH_%|
|**6**|**E/s do buffer**|PAGEIOLATCH_%|
|**7**|**Ocorrida***|RESOURCE_SEMAPHORE_QUERY_COMPILE|
|**8**|**SQL CLR**|% DE CLR, SQLCLR%|
|**9**|**Espelhamento**|DBMIRROR%|
|**10**|**Aciona**|TRANSAÇÃO%, DTC%, TRAN_MARKLATCH_%, MSQL_XACT_%, TRANSACTION_MUTEX|
|**11**|**Ocioso**|SLEEP_%, LAZYWRITER_SLEEP, SQLTRACE_BUFFER_FLUSH, SQLTRACE_INCREMENTAL_FLUSH_SLEEP, SQLTRACE_WAIT_ENTRIES, FT_IFTS_SCHEDULER_IDLE_WAIT, XE_DISPATCHER_WAIT, REQUEST_FOR_DEADLOCK_SEARCH, LOGMGR_QUEUE, ONDEMAND_TASK_QUEUE, CHECKPOINT_QUEUE, XE_TIMER_EVENT|
|**12**|**Preemptive**|PREEMPTIVE_%|
|**13**|**Service Broker**|BROKER_% **(mas não BROKER_RECEIVE_WAITFOR)**|
|**14**|**E/s de log Tran**|LOGMGR, LOGBUFFER, LOGMGR_RESERVE_APPEND, LOGMGR_FLUSH, LOGMGR_PMM_LOG, CHKPT, WRITELOG|
|**15**|**E/s de rede**|ASYNC_NETWORK_IO, NET_WAITFOR_PACKET, PROXY_NETWORK_IO EXTERNAL_SCRIPT_NETWORK_IOF|
|**16**|**Paralelismo**|ESPERAS CXPACKET, EXCHANGE, HT%, BMP%, BP%|
|**16**|**Memória**|RESOURCE_SEMAPHORE, CMEMTHREAD, CMEMPARTITIONED, EE_PMOLOCK, MEMORY_ALLOCATION_EXT, RESERVED_MEMORY_ALLOCATION_EXT, MEMORY_GRANT_UPDATE|
|**anos**|**Espera do usuário**|WAITFOR, WAIT_FOR_RESULTS, BROKER_RECEIVE_WAITFOR|
|**aprimora**|**Rastreamento**|TRACEWRITE, SQLTRACE_LOCK, SQLTRACE_FILE_BUFFER, SQLTRACE_FILE_WRITE_IO_COMPLETION, SQLTRACE_FILE_READ_IO_COMPLETION, SQLTRACE_PENDING_BUFFER_WRITERS, SQLTRACE_SHUTDOWN, QUERY_TRACEOUT, TRACE_EVTNOTIFF|
|**20,00**|**Pesquisa de Texto Completo**|FT_RESTART_CRAWL, GATHERER DE TEXTO COMPLETO, MSSEARCH, FT_METADATA_MUTEX, FT_IFTSHC_MUTEX, FT_IFTSISM_MUTEX, FT_IFTS_RWLOCK, FT_COMPROWSET_RWLOCK, FT_MASTER_MERGE, FT_PROPERTYLIST_CACHE, FT_MASTER_MERGE_COORDINATOR, PWAIT_RESOURCE_SEMAPHORE_FT_PARALLEL_QUERY_SYNC|
|**Abril**|**Outra e/s de disco**|ASYNC_IO_COMPLETION, IO_COMPLETION, BACKUPIO, WRITE_COMPLETION, IO_QUEUE_LIMIT, IO_RETRY|
|**22**|**Replicação**|SE_REPL_%, REPL_%, HADR_% **(mas não HADR_THROTTLE_LOG_RATE_GOVERNOR)**, PWAIT_HADR_%, REPLICA_WRITES, FCB_REPLICA_WRITE, FCB_REPLICA_READ, PWAIT_HADRSIM|
|**23**|**Administrador de taxa de log**|LOG_RATE_GOVERNOR, POOL_LOG_RATE_GOVERNOR, HADR_THROTTLE_LOG_RATE_GOVERNOR INSTANCE_LOG_RATE_GOVERNOR|

A categoria de espera de **compilação** não tem suporte no momento.

## <a name="permissions"></a>Permissões

 Requer a permissão `VIEW DATABASE STATE`.  
  
## <a name="see-also"></a>Consulte Também

- [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)
- [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)
- [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)
- [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)
- [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)
- [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)
- [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)
- [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)
- [Procedimentos Armazenados do Repositório de Consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
