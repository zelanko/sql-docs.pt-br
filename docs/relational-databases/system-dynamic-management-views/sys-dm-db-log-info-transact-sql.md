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
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sys.dm_db_log_info
- sys.dm_db_log_info_TSQL
- dm_db_log_info
- dm_db_log_info_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_db_log_info dynamic management view
ms.assetid: f6b40060-c17d-472f-b0a3-3b350275d487
caps.latest.revision: "4"
author: savjani
ms.author: pariks
manager: ajayj
ms.workload: Inactive
ms.openlocfilehash: b7250943f4e92d60888a75d9e577388f3cc6b1ed
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdbloginfo-transact-sql"></a>sys.dm_db_log_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Retorna `VLF` informações dos arquivos de log de transação. (Todos os arquivos de log são combinados na saída da tabela). Cada linha na saída representa um `VLF` no log de transações e fornece informações relevantes para esse VLF no log.

## <a name="syntax"></a>Sintaxe  
  
```  
sys.dm_db_log_info ( database_id )  
```  
## <a name="arguments"></a>Argumentos  
 *database_id* | NULO | PADRÃO  
 É a ID do banco de dados. *database_id* é **int**. As entradas válidas são o número de identificação de um banco de dados, NULL ou DEFAULT. O padrão é NULO. NULO e DEFAULT são valores equivalentes no contexto do banco de dados atual.
 
 Especifique NULL para retornar `VLF` informações do banco de dados atual.

 A função interna [DB_ID](../../t-sql/functions/db-id-transact-sql.md) pode ser especificado. Quando você usar DB_ID sem especificar um nome de banco de dados, o nível de compatibilidade do banco de dados atual deverá ser 90 ou mais.  

## <a name="table-returned"></a>Tabela retornada  

|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|ID do banco de dados.|
|file_id|**smallint**|Id do arquivo de log de transações.|  
|vlf_begin_offset|**bigint** |Deslocamento local do `VLF` desde o início do arquivo de log de transações.|
|vlf_size_mb |**float** |`VLF`tamanho em MB é arredondado para 2 casas decimais.|     
|vlf_sequence_number|**bigint** |`VLF`número de sequência na ordem de criação. Usado para identificar exclusivamente `VLFs` no arquivo de log.|
|vlf_active|**bit** |Indica se VLF está em uso ou não. <br />0 - vlf não está em uso.<br />1 - `VLF` está ativa.|
|vlf_status|**int** |Status de `VLF`. Os valores possíveis incluem <br />0 - `VLF` está inativo <br />1 - vlf é inicializado, mas não utilizado <br /> 2 - `VLF` está ativa.|
|vlf_parity|**tinyint** |Paridade de `VLF`. Usada internamente para determinar o final do log em um `VLF`.|
|vlf_first_lsn|**nvarchar(48)** |LSN do primeiro registro de log no `VLF`.|
|vlf_create_lsn|**nvarchar(48)** |LSN do log de registro que criou o `VLF`.|

## <a name="remarks"></a>Comentários
 O `sys.dm_db_log_info` função de gerenciamento dinâmico substitui o `DBCC LOGINFO` instrução. 
 
## <a name="permissions"></a>Permissões  
 Requer a `VIEW DATABASE STATE` no banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-determing-databases-in-a-sql-server-instance-with-high-number-of-vlfs"></a>A. Determinando os bancos de dados em uma instância do SQL Server com alto número de`VLFs`
A consulta a seguir determina os bancos de dados com mais de 100 `VLFs` nos arquivos de log, que pode afetar o tempo de inicialização, restauração e recuperação de banco de dados.

```sql
SELECT name,count(l.database_id) as 'vlf_count' from sys.databases s
cross apply sys.dm_db_log_info(s.database_id) l
group by name
having count(l.database_id)> 100
```

### <a name="b-determing-the-status-of-last-vlf-in-transaction-log-before-shrinking-the-log-file"></a>B. Determinando o status da última `VLF` no log de transações antes de reduzir o arquivo de log

A consulta a seguir pode ser usada para determinar o status da última `VLF` antes de executar shrinkfile no log de transações para determinar se pode reduzir o log de transações.

```sql
USE <database name>
GO

SELECT top 1 DB_NAME(database_id) as "Database Name",file_id,vlf_size_mb,vlf_sequence_number, vlf_active, vlf_status
from sys.dm_db_log_info(DEFAULT)
order by vlf_sequence_number desc
```


## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas ao &#40; do banco de dados Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_db_log_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)    
  



