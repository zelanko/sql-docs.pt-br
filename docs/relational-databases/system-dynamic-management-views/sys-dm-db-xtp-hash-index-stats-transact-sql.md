---
title: sys. dm_db_xtp_hash_index_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_hash_index_stats
- sys.dm_db_xtp_hash_index_stats_TSQL
- dm_db_xtp_hash_index_stats
- dm_db_xtp_hash_index_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_hash_index_stats (dynamic management view)
ms.assetid: 45969884-cd61-48e8-aee5-c725c78e3e4c
author: stevestein
ms.author: sstein
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f2bbaaaa6770c5644da227c7e64a9ff9e0fc2c13
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68026846"
---
# <a name="sysdm_db_xtp_hash_index_stats-transact-sql"></a>sys.dm_db_xtp_hash_index_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Essas estatísticas são úteis para entender e ajustar o número de buckets. Também pode ser usado para detectar os casos em que a chave de índice tem muitas duplicatas.  
  
 Um grande comprimento de cadeia média indica que várias linhas recebem o hash para o mesmo bucket. Isso pode acontecer porque:  
  
-   Se o número de buckets vazios for baixo ou os comprimentos de cadeia média e máxima forem semelhantes, é provável que o número total de buckets seja muito baixo. Isso faz as chaves de índice diferentes receberem o hash para o mesmo bucket.  
  
-   Se o número de buckets vazios for alto ou o comprimento máximo da cadeia for alto em relação ao comprimento de cadeia médio, é provável que haja várias linhas com valores de chave duplicados de índice ou haja uma distorção nos valores de chave. Todas as linhas com o mesmo valor de chave de índice recebem hash para o mesmo bucket; portanto, há um comprimento de cadeia longo nesse bucket.  
  
Os comprimentos de cadeia longos podem afetar significativamente o desempenho de todas as operações DML em linhas individuais, incluindo SELECT e INSERT. Os comprimentos de cadeias curtas com um número alto de buckets vazios estão na indicação de um bucket_count que seja muito alto. Isso diminui o desempenho de verificações de índice.  
  
> [!WARNING]
> **Sys. dm_db_xtp_hash_index_stats** examina a tabela inteira. Portanto, se houver grandes tabelas em seu banco de dados, **Sys. dm_db_xtp_hash_index_stats** poderá levar muito tempo.  
  
Para obter mais informações, consulte [índices de hash para tabelas com otimização de memória](../../relational-databases/sql-server-index-design-guide.md#hash_index).  
  
|Nome da coluna|Type|DESCRIÇÃO|  
|-----------------|----------|-----------------|  
|object_id|**int**|A ID de objeto da tabela pai.|  
|xtp_object_id|**bigint**|ID da tabela com otimização de memória.|  
|index_id|**int**|A ID do índice.|  
|total_bucket_count|**bigint**|O número total de buckets de hash no índice.|  
|empty_bucket_count|**bigint**|O número de bucket de hash vazio no índice.|  
|avg_chain_length|**bigint**|O comprimento médio das cadeias de linha em todos os buckets de hash no índice.|  
|max_chain_length|**bigint**|O comprimento máximo de cadeias de linha nos buckets de hash.|  
|xtp_object_id|**bigint**|A ID de objeto OLTP na memória que corresponde à tabela com otimização de memória.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DATABASE STATE no servidor.  

## <a name="examples"></a>Exemplos  
  
### <a name="a-troubleshooting-hash-index-bucket-count"></a>a. Solução de problemas de contagem de buckets do índice de hash

A consulta a seguir pode ser usada para solucionar o número de buckets de índice de hash de uma tabela existente. A consulta retorna estatísticas sobre a porcentagem de buckets vazios e o comprimento da cadeia para todos os índices de hash em tabelas do usuário.

```sql
  SELECT  
    QUOTENAME(SCHEMA_NAME(t.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(h.object_id)) as [table],   
    i.name                   as [index],   
    h.total_bucket_count,  
    h.empty_bucket_count,  
    FLOOR((  
      CAST(h.empty_bucket_count as float) /  
        h.total_bucket_count) * 100)  
                             as [empty_bucket_percent],  
    h.avg_chain_length,   
    h.max_chain_length  
  FROM sys.dm_db_xtp_hash_index_stats as h   
  INNER JOIN sys.indexes as i  
            ON h.object_id = i.object_id  
           AND h.index_id  = i.index_id  
    INNER JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
    INNER JOIN sys.tables t on h.object_id=t.object_id
  WHERE ia.type=1
  ORDER BY [table], [index];  
``` 

Para obter detalhes sobre como interpretar os resultados dessa consulta, consulte [Solucionando problemas de índices de hash para tabelas com otimização de memória](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md) .  

### <a name="b-hash-index-statistics-for-internal-tables"></a>B. Estatísticas de índice de hash para tabelas internas

Determinados recursos usam tabelas internas que aproveitam índices de hash, por exemplo, índices columnstore em tabelas com otimização de memória. A consulta a seguir retorna estatísticas para índices de hash em tabelas internas que estão vinculadas a tabelas de usuário.

```sql
  SELECT  
    QUOTENAME(SCHEMA_NAME(t.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(h.object_id)) as [user_table],
    ia.type_desc as [internal_table_type],
    i.name                   as [index],   
    h.total_bucket_count,  
    h.empty_bucket_count,  
    h.avg_chain_length,   
    h.max_chain_length  
  FROM sys.dm_db_xtp_hash_index_stats as h   
  INNER JOIN sys.indexes as i  
            ON h.object_id = i.object_id  
           AND h.index_id  = i.index_id  
    INNER JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
    INNER JOIN sys.tables t on h.object_id=t.object_id
  WHERE ia.type!=1
  ORDER BY [user_table], [internal_table_type], [index]; 
```

Observe que a BUCKET_COUNT do índice em tabelas internas não pode ser alterada, portanto, a saída dessa consulta deve ser considerada apenas informativa. Nenhuma ação é necessária.  

Essa consulta não deve retornar nenhuma linha, a menos que você esteja usando um recurso que aproveita índices de hash em tabelas internas. A tabela com otimização de memória a seguir contém um índice columnstore. Depois de criar essa tabela, você verá índices de hash em tabelas internas.

```sql
  CREATE TABLE dbo.table_columnstore
  (
    c1 INT NOT NULL PRIMARY KEY NONCLUSTERED,
    INDEX ix_columnstore CLUSTERED COLUMNSTORE
  ) WITH (MEMORY_OPTIMIZED=ON)
```

## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico de tabela com otimização de memória &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
