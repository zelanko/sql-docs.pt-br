---
title: sys. dm_db_log_space_usage (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_db_log_space_usage
- sys.dm_db_log_space_usage_TSQL
- dm_db_log_space_usage
- dm_db_log_space_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_log_space_usage dynamic management view
ms.assetid: f6b40060-c17d-472f-b0a3-3b350275d487
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bfa102163012456e9b2660d26cb54dec3d58cfbb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68264578"
---
# <a name="sysdm_db_log_space_usage-transact-sql"></a>sys. dm_db_log_space_usage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Retorna informações de uso de espaço para o log de transações. 
  
> [!NOTE]
> Todos os arquivos de log de transações são combinados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|database_id|**smallint**|ID do banco de dados.|  
|total_log_size_in_bytes |**bigint** |O tamanho do log  |
|used_log_space_in_bytes |**bigint** |O tamanho ocupado do log  |     
|used_log_space_in_percent |**real** |O tamanho ocupado do log como uma porcentagem do tamanho total do log |
|log_space_in_bytes_since_last_backup |**bigint** |A quantidade de espaço usada desde o último backup de log <br />**Aplica-se a:** [!INCLUDE[sssql14-md](../../includes/sssql14-md.md)] a [!INCLUDE[sscurrent-md](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|
    
  
## <a name="permissions"></a>Permissões  

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a `VIEW DATABASE STATE` permissão no banco de dados. Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-determine-the-amount-of-free-log-space-in-tempdb"></a>a. Determinar a quantidade de espaço livre de log em tempdb   
A consulta a seguir retorna o espaço de log livre total em megabytes (MB) disponível em tempdb.

```sql
USE tempdb;  
GO  

SELECT (total_log_size_in_bytes - used_log_space_in_bytes)*1.0/1024/1024 AS [free log space in MB]  
FROM sys.dm_db_log_space_usage;  
```
  
## <a name="see-also"></a>Consulte Também  
[Funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[Exibições de gerenciamento dinâmico relacionadas ao banco de dados &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys. dm_db_file_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)    
[sys. dm_db_task_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)   
[sys.dm_db_session_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)  
[sys. dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
[sys.dm_db_log_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md) 



