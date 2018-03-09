---
title: sys.query_store_runtime_stats_interval (Transact-SQL) | Microsoft Docs
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
- QUERY_STORE_RUNTIME_STATS_INTERVAL
- SYS.QUERY_STORE_RUNTIME_STATS_INTERVAL
- QUERY_STORE_RUNTIME_STATS_INTERVAL_TSQL
- SYS.QUERY_STORE_RUNTIME_STATS_INTERVAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.query_store_runtime_stats_interval catalog view
- query_store_runtime_stats_interval catalog view
ms.assetid: 2be83785-0569-41a3-88c8-59bfa0932e6e
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5891cdab36637b63dd24d4fd72f0f6a87b734769
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sysquerystoreruntimestatsinterval-transact-sql"></a>sys.query_store_runtime_stats_interval (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Contém informações sobre a hora de início e término de cada intervalo em tempo de execução de quais informações de estatísticas de execução para uma consulta foi coletadas.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**runtime_stats_interval_id**|**bigint**|Chave primária.|  
|**start_time**|**datetimeoffset**|Hora de início do intervalo.|  
|**end_time**|**datetimeoffset**|Hora de término do intervalo.|  
|**comentário**|**nvarchar (32)**|Sempre NULL.|  
  
## <a name="permissions"></a>Permissões  
 Requer o **VIEW DATABASE STATE** permissão.  
  
## <a name="see-also"></a>Consulte também  
 [database_query_store_options &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [query_store_plan &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [query_store_query &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [query_store_query_text &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [query_store_runtime_stats &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Repositório de consultas armazenadas procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
