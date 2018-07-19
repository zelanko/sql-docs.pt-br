---
title: sys.dm_db_log_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_log_stats_TSQL
- sys.dm_db_log_stats
- sys.dm_db_log_stats_TSQL
- dm_db_log_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_log_stats dynamic management function
ms.assetid: ''
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 018c02c2348e14028a5cbb84ef30b2428ac9e9e7
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38061444"
---
# <a name="sysdmdblogstats-transact-sql"></a>sys.dm_db_log_stats (Transact-SQL)   
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

Retorna atributos de nível de resumidos e informações sobre arquivos de log de transações de bancos de dados. Use essas informações para monitoramento e diagnóstico de integridade do log de transação.   
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
 sys.dm_db_log_stats ( database_id )
```  
  
## <a name="arguments"></a>Argumentos  

*database_id* | NULO | **Padrão**

É a ID do banco de dados. `database_id` é `int`. As entradas válidas são o número de identificação de um banco de dados `NULL`, ou `DEFAULT`. O padrão é `NULL`. `NULL` e `DEFAULT` são valores equivalentes no contexto do banco de dados atual.  
A função interna [DB_ID](../../t-sql/functions/db-id-transact-sql.md) pode ser especificado. Ao usar `DB_ID` sem especificar um nome de banco de dados, o nível de compatibilidade do banco de dados atual deve ser 90 ou superior.

  
## <a name="tables-returned"></a>Tabelas retornadas  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|database_id    |**int**    |ID do banco de dados |  
|recovery_model |**nvarchar(60)**   |   Modelo de recuperação do banco de dados. Os valores possíveis incluem: <br /> SIMPLE<br /> BULK_LOGGED <br /> FULL |  
|log_min_lsn    |**nvarchar(24)**   |   Início atual [(LSN) do número de sequência de log](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) no log de transações.|  
|log_end_lsn    |**nvarchar(24)**   |   [log (LSN) do número de sequência](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) do último registro de log no log de transações.|  
|current_vlf_sequence_number    |**bigint** |   Atual [(VLF) do arquivo de log virtual](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) número de sequência no momento da execução.|  
|current_vlf_size_mb    |**float**  |   Atual [(VLF) do arquivo de log virtual](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) tamanho em MB.|   
|total_vlf_count    |**bigint** |   Número total de [(VLFs) de arquivos de log virtuais](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) no log de transações. |  
|total_log_size_mb  |**float**  |   Tamanho do log de transação total em MB. |  
|active_vlf_count   |**bigint** |   Número total de ativos [(VLFs) de arquivos de log virtuais](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) no log de transações.|  
|active_log_size_mb |**float**  |   Tamanho do log de transação ativa total em MB.|  
|log_truncation_holdup_reason   |**nvarchar(60)**   |   Razão de retenção de truncamento de log. O valor é o mesmo que `log_reuse_wait_desc` coluna de `sys.databases`.  (Para obter mais explicações sobre esses valores, consulte [o Log de transações](../../relational-databases/logs/the-transaction-log-sql-server.md)). <br />Os valores possíveis incluem: <br />NOTHING<br />CHECKPOINT<br />LOG_BACKUP<br />ACTIVE_BACKUP_OR_RESTORE<br />ACTIVE_TRANSACTION<br />DATABASE_MIRRORING<br />Replicação<br />DATABASE_SNAPSHOT_CREATION<br />LOG_SCAN<br />AVAILABILITY_REPLICA<br />OLDEST_PAGE<br />XTP_CHECKPOINT<br />OUTRO TRANSITÓRIO |  
|log_backup_time    |**datetime**   |   Transaction log hora do último backup.|   
|log_backup_lsn |**nvarchar(24)**   |   Último backup de log de transações [(LSN) do número de sequência de log](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch).|   
|log_since_last_log_backup_mb   |**float**  |   Tamanho do log em MB, desde o último backup de log de transações [(LSN) do número de sequência de log](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch).|  
|log_checkpoint_lsn |**nvarchar(24)**   |   Último ponto de verificação [(LSN) do número de sequência de log](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch).|  
|log_since_last_checkpoint_mb   |**float**  |   Tamanho do log em MB, desde o último ponto de verificação [(LSN) do número de sequência de log](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch).|  
|log_recovery_lsn   |**nvarchar(24)**   |   Recuperação [(LSN) do número de sequência de log](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) do banco de dados. Se `log_recovery_lsn` ocorre antes do ponto de verificação LSN, `log_recovery_lsn` é a transação ativa mais antiga LSN, caso contrário, `log_recovery_lsn` é o LSN do ponto de verificação.|  
|log_recovery_size_mb   |**float**  |   Tamanho do log em MB, desde a recuperação de log [(LSN) do número de sequência de log](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch).|  
|recovery_vlf_count |**bigint** |   Número total de [arquivos de log virtuais (VLFs)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) sejam recuperados, se houver failover ou reinicialização de servidor. |  


## <a name="permissions"></a>Permissões  
Requer a `VIEW DATABASE STATE` permissão no banco de dados.   
  
## <a name="examples"></a>Exemplos  

### <a name="a-determining-databases-in-a-includessnoversionincludesssnoversion-mdmd-instance-with-high-number-of-vlfs"></a>A. Determinando os bancos de dados em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância com um grande número de VLFs   
A consulta a seguir retorna os bancos de dados com mais de 100 VLFs nos arquivos de log. Grande número de VLFs pode afetar o tempo de inicialização, restauração e recuperação de banco de dados.

```sql  
SELECT name AS 'Database Name', total_vlf_count AS 'VLF count' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id) 
WHERE total_vlf_count  > 100;
```   

### <a name="b-determining-databases-in-a-includessnoversionincludesssnoversion-mdmd-instance-with-transaction-log-backups-older-than-4-hours"></a>B. Determinando os bancos de dados em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância com backups de log de transações com mais de 4 horas   
A consulta a seguir determina os últimos tempos de backup de log para bancos de dados na instância.

```sql  
SELECT name AS 'Database Name', log_backup_time AS 'last log backup time' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id); 
```

## <a name="see-also"></a>Consulte também  
[Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[Banco de dados relacionados a exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
  
