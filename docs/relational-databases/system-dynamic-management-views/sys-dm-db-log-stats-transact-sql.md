---
description: sys.dm_db_log_stats (Transact-SQL)
title: sys. dm_db_log_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 98c8b45ccde39b7155443b1ef7fabd994f6b26ab
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550290"
---
# <a name="sysdm_db_log_stats-transact-sql"></a>sys.dm_db_log_stats (Transact-SQL)   
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

Retorna atributos de nível de resumo e informações sobre arquivos de log de transações de bancos de dados. Use essas informações para monitoramento e diagnóstico da integridade do log de transações.   
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
 sys.dm_db_log_stats ( database_id )
```  
  
## <a name="arguments"></a>Argumentos  

*database_id* | NULL | **Padrão**

É a ID do banco de dados. `database_id` é `int`. As entradas válidas são o número de identificação de um banco de dados, `NULL` ou `DEFAULT` . O padrão é `NULL`. `NULL` e `DEFAULT` são valores equivalentes no contexto do banco de dados atual.  
A função interna [DB_ID](../../t-sql/functions/db-id-transact-sql.md) pode ser especificada. Ao usar `DB_ID` sem especificar um nome de banco de dados, o nível de compatibilidade do banco de dados atual deve ser 90 ou superior.

  
## <a name="tables-returned"></a>Tabelas retornadas  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|database_id    |**int**    |ID do banco de dados |  
|recovery_model |**nvarchar(60)**   |   Modelo de recuperação do banco de dados. Os valores possíveis incluem: <br /> SIMPLES<br /> BULK_LOGGED <br /> FULL |  
|log_min_lsn    |**nvarchar (24)**   |   [LSN (número de sequência de log)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) inicial atual no log de transações.|  
|log_end_lsn    |**nvarchar (24)**   |   [LSN (número de sequência de log)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) do último registro de log no log de transações.|  
|current_vlf_sequence_number    |**bigint** |   Número de sequência do [arquivo de log virtual (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) atual no momento da execução.|  
|current_vlf_size_mb    |**float**  |   Tamanho atual do [arquivo de log virtual (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) em MB.|   
|total_vlf_count    |**bigint** |   Número total de [arquivos de log virtuais (VLFs)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) no log de transações. |  
|total_log_size_mb  |**float**  |   Tamanho total do log de transações em MB. |  
|active_vlf_count   |**bigint** |   Número total de [arquivos de log virtuais ativos (VLFs)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) no log de transações.|  
|active_log_size_mb |**float**  |   Tamanho total do log de transações ativas em MB.|  
|log_truncation_holdup_reason   |**nvarchar(60)**   |   Motivo de retenção de truncamento de log. O valor é o mesmo que a  `log_reuse_wait_desc` coluna de `sys.databases` .  (Para obter explicações mais detalhadas sobre esses valores, consulte [o log de transações](../../relational-databases/logs/the-transaction-log-sql-server.md)). <br />Os valores possíveis incluem: <br />NOTHING<br />CHECKPOINT<br />LOG_BACKUP<br />ACTIVE_BACKUP_OR_RESTORE<br />ACTIVE_TRANSACTION<br />DATABASE_MIRRORING<br />REPLICAÇÃO<br />DATABASE_SNAPSHOT_CREATION<br />LOG_SCAN<br />AVAILABILITY_REPLICA<br />OLDEST_PAGE<br />XTP_CHECKPOINT<br />OUTROS TRANSITÓRIOS |  
|log_backup_time    |**datetime**   |   Hora do último backup do log de transações.|   
|log_backup_lsn |**nvarchar (24)**   |   [Número de sequência do log de backup do último log de transações (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch).|   
|log_since_last_log_backup_mb   |**float**  |   Tamanho do log em MB desde o último [número de sequência do log](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)de backup do log de transações (LSN).|  
|log_checkpoint_lsn |**nvarchar (24)**   |   [LSN (número de sequência de log) do](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)último ponto de verificação.|  
|log_since_last_checkpoint_mb   |**float**  |   Tamanho do log em MB desde o último [número de sequência de log do ponto de verificação (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch).|  
|log_recovery_lsn   |**nvarchar (24)**   |   [LSN (número de sequência de log](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) de recuperação) do banco de dados. Se `log_recovery_lsn` ocorrer antes do LSN do ponto de verificação, `log_recovery_lsn` será o LSN de transação ativa mais antigo, caso contrário, `log_recovery_lsn` será o LSN do ponto de verificação.|  
|log_recovery_size_mb   |**float**  |   Tamanho do log em MB desde o [LSN (número de sequência do log de recuperação de log)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch).|  
|recovery_vlf_count |**bigint** |   Número total de [arquivos de log virtuais (VLFs)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) a serem recuperados, se houver failover ou reinicialização do servidor. |  


## <a name="remarks"></a>Comentários
Ao executar `sys.dm_db_log_stats` em um banco de dados que participa de um grupo de disponibilidade como uma réplica secundária, apenas um subconjunto dos campos descritos acima será retornado.  Atualmente, somente `database_id` , `recovery_model` e `log_backup_time` será retornado quando executado em um banco de dados secundário.   

## <a name="permissions"></a>Permissões  
Requer a `VIEW DATABASE STATE` permissão no banco de dados.   
  
## <a name="examples"></a>Exemplos  

### <a name="a-determining-databases-in-a-ssnoversion-instance-with-high-number-of-vlfs"></a>a. Determinando bancos de dados em uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância com um número alto de VLFs   
A consulta a seguir retorna os bancos de dados com mais de 100 VLFs nos arquivos de log. Grandes números de VLFs podem afetar a inicialização, a restauração e o tempo de recuperação do banco de dados.

```sql  
SELECT name AS 'Database Name', total_vlf_count AS 'VLF count' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id) 
WHERE total_vlf_count  > 100;
```   

### <a name="b-determining-databases-in-a-ssnoversion-instance-with-transaction-log-backups-older-than-4-hours"></a>B. Determinando bancos de dados em uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância com backups de log de transações com mais de 4 horas   
A consulta a seguir determina as horas de backup do último log para os bancos de dados na instância.

```sql  
SELECT name AS 'Database Name', log_backup_time AS 'last log backup time' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id); 
```

## <a name="see-also"></a>Consulte Também  
[Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[Exibições de gerenciamento dinâmico relacionadas ao banco de dados &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
  
