---
title: sys.dm_db_log_info (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 
author: savjani
ms.author: pariks
manager: ajayj
ms.workload: Inactive
ms.openlocfilehash: 661647715d2fcff3a4821250dfaa65e0fea07d6e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="sysdmdbloginfo-transact-sql"></a>sys.dm_db_log_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Retorna [(VLF) do arquivo de log virtual](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) informações do log de transações. Observe que todos os arquivos de log de transações são combinados na saída da tabela. Cada linha na saída representa um VLF no log de transações e fornece informações relevantes para esse VLF no log.

## <a name="syntax"></a>Sintaxe  
  
```  
sys.dm_db_log_info ( database_id )  
```  
## <a name="arguments"></a>Argumentos  
 *database_id* | NULO | PADRÃO  
 É a ID do banco de dados. *database_id* é **int**. As entradas válidas são o número de identificação de um banco de dados, NULL ou DEFAULT. O padrão é NULO. NULO e DEFAULT são valores equivalentes no contexto do banco de dados atual.
 
 Especifique NULL para retornar informações de VLF do banco de dados atual.

 A função interna [DB_ID](../../t-sql/functions/db-id-transact-sql.md) pode ser especificado. Ao usar `DB_ID` sem especificar um nome de banco de dados, o nível de compatibilidade do banco de dados atual deve ser 90 ou superior.  

## <a name="table-returned"></a>Tabela retornada  

|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|ID do banco de dados.|
|file_id|**smallint**|Id do arquivo de log de transações.|  
|vlf_begin_offset|**bigint** |Deslocamento local do [(VLF) do arquivo de log virtual](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) desde o início do arquivo de log de transações.|
|vlf_size_mb |**float** |[arquivo de log virtual (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) tamanho em MB, arredondado para 2 casas decimais.|     
|vlf_sequence_number|**bigint** |[arquivo de log virtual (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) número na ordem de criação de sequência. Usado para identificar exclusivamente VLFs no arquivo de log.|
|vlf_active|**bit** |Indica se [(VLF) do arquivo de log virtual](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) está em uso ou não. <br />0 - VLF não está em uso.<br />1 - VLF está ativa.|
|vlf_status|**int** |Status de [(VLF) do arquivo de log virtual](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch). Os valores possíveis incluem <br />0 - VLF está inativo <br />1 - VLF é inicializado, mas não utilizado <br /> 2 - VLF está ativa.|
|vlf_parity|**tinyint** |Paridade de [(VLF) do arquivo de log virtual](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch). Usada internamente para determinar o final do log em um VLF.|
|vlf_first_lsn|**nvarchar(48)** |[Log (LSN) do número de sequência](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) do primeiro registro de log no [(VLF) do arquivo de log virtual](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch).|
|vlf_create_lsn|**nvarchar(48)** |[Log (LSN) do número de sequência](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) do log de eventos que criou o [(VLF) do arquivo de log virtual](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch).|

## <a name="remarks"></a>Remarks
 O `sys.dm_db_log_info` função de gerenciamento dinâmico substitui o `DBCC LOGINFO` instrução. 
 
## <a name="permissions"></a>Permissões  
 Requer a `VIEW DATABASE STATE` no banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-determing-databases-in-a-sql-server-instance-with-high-number-of-vlfs"></a>A. Determinando os bancos de dados em uma instância do SQL Server com um número alto de VLFs
A consulta a seguir determina os bancos de dados com mais de 100 VLFs nos arquivos de log, que podem afetar o tempo de inicialização, restauração e recuperação de banco de dados.

```sql
SELECT [name], COUNT(l.database_id) AS 'vlf_count' 
FROM sys.databases s
CROSS APPLY sys.dm_db_log_info(s.database_id) l
GROUP BY [name]
HAVING COUNT(l.database_id) > 100
```

### <a name="b-determing-the-status-of-last-vlf-in-transaction-log-before-shrinking-the-log-file"></a>B. Determinando o status da última `VLF` no log de transações antes de reduzir o arquivo de log

A consulta a seguir pode ser usada para determinar o status do último VLF antes de executar shrinkfile no log de transações para determinar se o log de transações pode ser reduzido.

```sql
USE AdventureWorks2016
GO

SELECT TOP 1 DB_NAME(database_id) AS "Database Name", file_id, vlf_size_mb, vlf_sequence_number, vlf_active, vlf_status
FROM sys.dm_db_log_info(DEFAULT)
ORDER BY vlf_sequence_number DESC
```


## <a name="see-also"></a>Consulte Também  
[Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[Exibições de gerenciamento dinâmico relacionadas ao &#40; do banco de dados Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_stats &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)

