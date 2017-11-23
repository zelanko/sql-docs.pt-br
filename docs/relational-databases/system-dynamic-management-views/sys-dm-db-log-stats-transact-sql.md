---
title: sys.dm_db_log_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_db_log_stats_TSQL
- sys.dm_db_log_stats
- sys.dm_db_log_stats_TSQL
- dm_db_log_stats
dev_langs: TSQL
helpviewer_keywords: sys.dm_db_log_stats dynamic management function
ms.assetid: 
caps.latest.revision: 
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ba933bad47beead99ea5f645a910b1783caa280e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdblogstats-transact-sql"></a>sys.dm_db_log_stats (Transact-SQL)   
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Retorna atributos de nível de resumos e as informações sobre arquivos de log de transações de bancos de dados. Use essas informações para monitoramento e diagnóstico de integridade do log de transações.   
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
 sys.dm_db_log_stats ( database_id )
```  
  
## <a name="arguments"></a>Argumentos  

*database_id* | NULO | **Padrão**

É a ID do banco de dados. `database_id`is `int`. As entradas válidas são o número de identificação de um banco de dados, `NULL`, ou `DEFAULT`. O padrão é `NULL`. `NULL`e `DEFAULT` são valores equivalentes no contexto do banco de dados atual.  
A função interna `DB_ID` pode ser especificado. Ao usar `DB_ID` sem especificar um nome de banco de dados, o nível de compatibilidade do banco de dados atual deve ser 90 ou superior.

  
## <a name="tables-returned"></a>Tabelas retornadas  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|database_id    |**int**    |ID do banco de dados |  
|recovery_model |**nvarchar (60)**   |   Modelo de recuperação do banco de dados. Os valores possíveis incluem: <br /> SIMPLE<br /> BULK_LOGGED <br /> FULL |  
|log_min_lsn    |**nvarchar(24)**   |   Início atual LSN no log de transações. |  
|log_end_lsn    |**nvarchar(24)**   |   LSN do último registro de log no log de transações. |  
|current_vlf_sequence_number    |**bigint** |   VLF número de sequência atual no momento da execução. |  
|current_vlf_size_mb    |**float**  |   Tamanho atual de VLF em MB. |   
|total_vlf_count    |**bigint** |   Número total de VLFs no log de transações. |  
|total_log_size_mb  |**float**  |   Tamanho do log de transações total em MB. |  
|active_vlf_count   |**bigint** |   Número total de ativos VLFs no log de transações. |  
|active_log_size_mb |**float**  |   Tamanho do log de transação ativa total em MB. |  
|log_truncation_holdup_reason   |**nvarchar (60)**   |   Razão de retenção de truncamento do log. O valor é igual a `log_reuse_wait_desc` coluna `sys.databases`.  (Para obter mais explicações sobre esses valores, consulte [o Log de transações](../../relational-databases/logs/the-transaction-log-sql-server.md)). <br />Os valores possíveis incluem: <br />NOTHING<br />CHECKPOINT<br />LOG_BACKUP<br />ACTIVE_BACKUP_OR_RESTORE<br />ACTIVE_TRANSACTION<br />DATABASE_MIRRORING<br />Replicação<br />DATABASE_SNAPSHOT_CREATION<br />LOG_SCAN<br />AVAILABILITY_REPLICA<br />OLDEST_PAGE<br />XTP_CHECKPOINT<br />OUTRO TRANSITÓRIO |  
|log_backup_time    |**datetime**   |   Transaction log horário do último backup. |   
|log_backup_lsn |**nvarchar(24)**   |   Último backup de log de transação LSN. |   
|log_since_last_log_backup_mb   |**float**  |   Tamanho do log em MB desde o último backup de log de transação LSN. |  
|log_checkpoint_lsn |**nvarchar(24)**   |   Último ponto de verificação LSN. |  
|log_since_last_checkpoint_mb   |**float**  |   Tamanho do log em MB desde o último ponto de verificação LSN. |  
|log_recovery_lsn   |**nvarchar(24)**   |   LSN do banco de dados de recuperação. Se `log_recovery_lsn` ocorre antes do ponto de verificação LSN, `log_recovery_lsn` é a transação ativa mais antiga LSN, caso contrário, `log_recovery_lsn` é o LSN do ponto de verificação. |  
|log_recovery_size_mb   |**float**  |   Tamanho do log em MB desde o LSN de recuperação de log. |  
|recovery_vlf_count |**bigint** |   Número total de VLFs serão recuperados, se não houver failover ou reinicialização de servidor. |  


## <a name="permissions"></a>Permissões  
Requer a `VIEW DATABASE STATE` no banco de dados.   
  
## <a name="examples"></a>Exemplos  

### <a name="a-determining-databases-in-a-includessnoversionincludesssnoversion-mdmd-instance-with-high-number-of-vlfs"></a>A. Determinando os bancos de dados em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância com um número alto de vlfs   
A consulta a seguir retorna os bancos de dados com mais de 100 vlfs nos arquivos de log. Grandes números de VLFs podem afetar o tempo de inicialização, restauração e recuperação de banco de dados.

``` t-sql  
SELECT name AS 'Database Name', total_vlf_count AS 'VLF count' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id) 
WHERE total_vlf_count  > 100;
```   

### <a name="b-determining-databases-in-a-includessnoversionincludesssnoversion-mdmd-instance-with-transaction-log-backups-older-than-4-hours"></a>B. Determinando os bancos de dados em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância com backups de log de transações com mais de 4 horas   
A consulta a seguir determina os último tempos de backup de log para os bancos de dados na instância.

``` t-sql  
SELECT name AS 'Database Name', log_backup_time AS 'last log backup time' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id); 
```

## <a name="see-also"></a>Consulte também  
[Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[Exibições de gerenciamento dinâmico relacionadas ao &#40; do banco de dados Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)  

  
