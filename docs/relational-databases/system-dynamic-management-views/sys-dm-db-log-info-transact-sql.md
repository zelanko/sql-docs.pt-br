---
title: sys. dm_db_log_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_db_log_info
- sys.dm_db_log_info_TSQL
- dm_db_log_info
- dm_db_log_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_log_info dynamic management view
ms.assetid: f6b40060-c17d-472f-b0a3-3b350275d487
author: savjani
ms.author: pariks
manager: ajayj
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7cb87d2d5677085edc8e6bd998f20c3c45013823
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68262076"
---
# <a name="sysdm_db_log_info-transact-sql"></a>sys. dm_db_log_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

Retorna informações de [VLF (arquivo de log virtual)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) do log de transações. Observe que todos os arquivos de log de transações são combinados na saída da tabela. Cada linha na saída representa um VLF no log de transações e fornece informações relevantes para esse VLF no log.

## <a name="syntax"></a>Sintaxe  
  
```  
sys.dm_db_log_info ( database_id )  
``` 

## <a name="arguments"></a>Argumentos  
 *database_id* | NULL | OS  
 É a ID do banco de dados. *database_id* é **int**. As entradas válidas são o número de identificação de um banco de dados, nulo ou padrão. O padrão é NULO. NULL e DEFAULT são valores equivalentes no contexto do banco de dados atual.
 
 Especifique NULL para retornar informações de VLF do banco de dados atual.

 A função interna [DB_ID](../../t-sql/functions/db-id-transact-sql.md) pode ser especificada. Ao usar `DB_ID` sem especificar um nome de banco de dados, o nível de compatibilidade do banco de dados atual deve ser 90 ou superior.  

## <a name="table-returned"></a>Tabela retornada  

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|database_id|**int**|ID do banco de dados.|
|file_id|**smallint**|ID de arquivo do log de transações.|  
|vlf_begin_offset|**bigint** |O local de deslocamento do [arquivo de log virtual (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) do início do arquivo de log de transações.|
|vlf_size_mb |**float** |tamanho do [arquivo de log virtual (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) em MB, arredondado para 2 casas decimais.|     
|vlf_sequence_number|**bigint** |número de sequência do [arquivo de log virtual (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) na ordem criada. Usado para identificar exclusivamente VLFs no arquivo de log.|
|vlf_active|**bit** |Indica se o [arquivo de log virtual (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) está em uso ou não. <br />0-VLF não está em uso.<br />1-VLF está ativo.|
|vlf_status|**int** |Status do [arquivo de log virtual (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch). Os valores possíveis incluem <br />0-VLF está inativo <br />1-VLF é inicializado, mas não usado <br /> 2-VLF está ativo.|
|vlf_parity|**tinyint** |Paridade do [arquivo de log virtual (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch). Usado internamente para determinar o final do log em um VLF.|
|vlf_first_lsn|**nvarchar (48)** |O [LSN (número de sequência de log)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) do primeiro registro de log no [arquivo de log virtual (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch).|
|vlf_create_lsn|**nvarchar (48)** |[LSN (número de sequência de log)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) do registro de log que criou o [arquivo de log virtual (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch).|
|vlf_encryptor_thumbprint|**varbinary(20)**| **Aplica-se a:** [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] <br><br> Mostra a impressão digital do criptografador do VLF se o VLF for criptografado usando [Transparent Data Encryption](../../relational-databases/security/encryption/transparent-data-encryption.md), caso contrário, NULL. |

## <a name="remarks"></a>Comentários
A `sys.dm_db_log_info` função de gerenciamento dinâmico substitui `DBCC LOGINFO` a instrução.    
 
## <a name="permissions"></a>Permissões  
Requer a `VIEW DATABASE STATE` permissão no banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-determing-databases-in-a-sql-server-instance-with-high-number-of-vlfs"></a>a. Determo bancos de dados em uma instância SQL Server com um número alto de VLFs
A consulta a seguir determina os bancos de dados com mais de 100 VLFs nos arquivos de log, o que pode afetar a inicialização, a restauração e o tempo de recuperação do banco de dados.

```sql
SELECT [name], COUNT(l.database_id) AS 'vlf_count' 
FROM sys.databases s
CROSS APPLY sys.dm_db_log_info(s.database_id) l
GROUP BY [name]
HAVING COUNT(l.database_id) > 100
```

### <a name="b-determing-the-position-of-the-last-vlf-in-transaction-log-before-shrinking-the-log-file"></a>B. Determo a posição do último `VLF` no log de transações antes de reduzir o arquivo de log

A consulta a seguir pode ser usada para determinar a posição do último VLF ativo antes de executar o SHRINKFILE no log de transações para determinar se o log de transações pode ser reduzido.

```sql
USE AdventureWorks2016
GO

;WITH cte_vlf AS (
SELECT ROW_NUMBER() OVER(ORDER BY vlf_begin_offset) AS vlfid, DB_NAME(database_id) AS [Database Name], vlf_sequence_number, vlf_active, vlf_begin_offset, vlf_size_mb
    FROM sys.dm_db_log_info(DEFAULT)),
cte_vlf_cnt AS (SELECT [Database Name], COUNT(vlf_sequence_number) AS vlf_count,
    (SELECT COUNT(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 0) AS vlf_count_inactive,
    (SELECT COUNT(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 1) AS vlf_count_active,
    (SELECT MIN(vlfid) FROM cte_vlf WHERE vlf_active = 1) AS ordinal_min_vlf_active,
    (SELECT MIN(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 1) AS min_vlf_active,
    (SELECT MAX(vlfid) FROM cte_vlf WHERE vlf_active = 1) AS ordinal_max_vlf_active,
    (SELECT MAX(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 1) AS max_vlf_active
    FROM cte_vlf
    GROUP BY [Database Name])
SELECT [Database Name], vlf_count, min_vlf_active, ordinal_min_vlf_active, max_vlf_active, ordinal_max_vlf_active,
((ordinal_min_vlf_active-1)*100.00/vlf_count) AS free_log_pct_before_active_log,
((ordinal_max_vlf_active-(ordinal_min_vlf_active-1))*100.00/vlf_count) AS active_log_pct,
((vlf_count-ordinal_max_vlf_active)*100.00/vlf_count) AS free_log_pct_after_active_log
FROM cte_vlf_cnt
GO
```

## <a name="see-also"></a>Consulte Também  
[Funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[Exibições de gerenciamento dinâmico relacionadas ao banco de dados &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys. dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)

