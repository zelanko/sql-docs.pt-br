---
title: sys.dm_db_log_space_usage (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sys.dm_db_log_space_usage
- sys.dm_db_log_space_usage_TSQL
- dm_db_log_space_usage
- dm_db_log_space_usage_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_db_log_space_usage dynamic management view
ms.assetid: f6b40060-c17d-472f-b0a3-3b350275d487
caps.latest.revision: "4"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f7e0e14e96c3581b7a66fad23e21ac7a15808a1f
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="sysdmdblogspaceusage-transact-sql"></a>sys.dm_db_log_space_usage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna informações de uso para o log de banco de dados de espaço. (Todos os arquivos de log são combinados.) 
  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|database_id|**smallint**|ID do banco de dados.|  
|total_log_size_in_bytes |**bigint** |O tamanho do log  |
|used_log_space_in_bytes |**bigint** |O tamanho de ocupado do log  |     
|used_log_space_in_percent |**real** |O tamanho de ocupado do log como uma porcentagem do tamanho total de log |
|log_space_in_bytes_since_last_backup |**bigint** |A quantidade de espaço usado desde o último backup de log <br />**Aplica-se a:** [!INCLUDE[sssql14-md](../../includes/sssql14-md.md)] por meio de [!INCLUDE[sscurrent-md](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|
    
  
## <a name="permissions"></a>Permissões  
 Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer `VIEW SERVER STATE` permissão no servidor.  
  
 Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)] as camadas Premium requerem o `VIEW DATABASE STATE` no banco de dados. Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)] camadas Standard e Basic requer o [!INCLUDE[ssSDS](../../includes/sssds-md.md)] conta de administrador.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-determine-the-amount-of-free-log-space-in-tempdb"></a>A. Determinar a quantidade de Log de espaço livre em tempdb   
A consulta a seguir retorna o espaço livre total de log em megabytes (MB) disponível em tempdb.

```sql
USE tempdb;  
GO  

SELECT (total_log_size_in_bytes - used_log_space_in_bytes)*1.0/1024/1024 AS [free log space in MB]  
FROM sys.dm_db_log_space_usage;  
```
  
## <a name="see-also"></a>Consulte Também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas ao &#40; do banco de dados Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [sys.DM db_file_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)    
 [sys.DM db_task_space_usage &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)   
 [sys.dm_db_session_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)  
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md) 



