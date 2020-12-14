---
description: sys.query_store_runtime_stats_interval (Transact-SQL)
title: sys.query_store_runtime_stats_interval (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 49c45098a319a3a9577fe5911ac1f5f0accc6990
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97404237"
---
# <a name="sysquery_store_runtime_stats_interval-transact-sql"></a>sys.query_store_runtime_stats_interval (Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  Contém informações sobre a hora de início e de término de cada intervalo sobre o qual as informações de estatísticas de execução de tempo de execução de uma consulta foram coletadas.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**runtime_stats_interval_id**|**bigint**|Chave primária.|
|**start_time**|**datetimeoffset**|Hora de início do intervalo.|
|**end_time**|**datetimeoffset**|Hora de término do intervalo.|
|**mente**|**nvarchar(32)**|Sempre nulo.|
  
## <a name="permissions"></a>Permissões  
 Requer a permissão **View Database State** .  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sys.database_query_store_options ](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.query_context_settings ](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.query_store_plan ](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.query_store_query ](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.query_store_query_text ](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.query_store_runtime_stats ](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Procedimentos Armazenados do Repositório de Consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
