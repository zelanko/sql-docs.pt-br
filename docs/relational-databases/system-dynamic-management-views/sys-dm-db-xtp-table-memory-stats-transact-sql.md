---
title: sys.dm_db_xtp_table_memory_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_table_memory_stats_TSQL
- dm_db_xtp_table_memory_stats
- sys.dm_db_xtp_table_memory_stats
- dm_db_xtp_table_memory_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_table_memory_stats
- dm_db_xtp_table_memory_stats
ms.assetid: ad0efc06-3d9c-4861-9dfa-a7a87822d0c8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8ade5650c1c47f6d52602b04f14af3ad79dbe609
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47808504"
---
# <a name="sysdmdbxtptablememorystats-transact-sql"></a>sys.dm_db_xtp_table_memory_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Retorna estatísticas de uso da memória para cada tabela [!INCLUDE[hek_2](../../includes/hek-2-md.md)] (usuário e sistema) no banco de dados atual. As tabelas do sistema têm IDs de objeto negativas e são usadas para armazenar informações de tempo de execução do mecanismo [!INCLUDE[hek_2](../../includes/hek-2-md.md)]. Diferentemente dos objetos de usuário, as tabelas do sistema são internas e só existem na memória, portanto, não podem ser visualizadas por meio de exibições do catálogo. As tabelas do sistema são usadas para armazenar informações como metadados de todos os arquivos de dados/delta no armazenamento, mesclar solicitações, marcas d'água para arquivos delta para filtros de linha, tabelas removidas e informações relevantes para recuperação e backups. Considerando que o mecanismo [!INCLUDE[hek_2](../../includes/hek-2-md.md)] pode ter até 8.192 pares de arquivos de dados e delta, para bancos de dados grandes na memória, a memória usada pelas tabelas do sistema podem ter alguns megabytes.  
  
 Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|A ID de objeto da tabela. NULL para tabelas do sistema OLTP na memória.|  
|memory_allocated_for_table_kb|**bigint**|Memória alocada para essa tabela.|  
|memory_used_by_table_kb|**bigint**|Memória usada pela tabela, incluindo versões de linha.|  
|memory_allocated_for_indexes_kb|**bigint**|Memória alocada para índices nessa tabela.|  
|memory_used_by_indexes_kb|**bigint**|Memória consumida para índices nessa tabela.|  
  
## <a name="permissions"></a>Permissões  
 Todas as linhas são retornadas se você tiver a permissão VIEW DATABASE STATE no banco de dados atual. Caso contrário, um conjunto de linhas vazio será retornado.  
  
 Se você não tiver permissão VIEW DATABASE, todas as colunas serão retornadas para as linhas nas tabelas nas quais você tiver permissão SELECT.  
  
 As tabelas do sistema são retornadas apenas para usuários com permissão VIEW DATABASE STATE.  
  
## <a name="examples"></a>Exemplos  
 Você pode consultar a seguinte DMV para obter a memória alocada para as tabelas e os índices no banco de dados:  
  
```  
-- finding memory for objects  
SELECT OBJECT_NAME(object_id), *   
FROM sys.dm_db_xtp_table_memory_stats;  
```  
  
 Para localizar a memória de todos os objetos no banco de dados:  
  
```  
SELECT SUM( memory_allocated_for_indexes_kb + memory_allocated_for_table_kb) AS  
 memoryallocated_objects_in_kb   
FROM sys.dm_db_xtp_table_memory_stats;  
```  
  
## <a name="user-scenario"></a>Cenário de uso  
 Primeiro crie as seguintes tabelas em um banco de dados chamado HkDb1.  
  
```  
-- set max server memory to 4 GB  
EXEC sp_configure 'max server memory (MB)', 4048  
go  
  
RECONFIGURE  
go  
  
-- create a resource pool for database with memory-optimized objects  
CREATE RESOURCE POOL PoolHkDb1 WITH (MAX_MEMORY_PERCENT = 50);  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
go  
  
--bind the pool to the database  
EXEC sp_xtp_bind_db_resource_pool 'HkDb1', 'PoolHkdb1'  
go  
  
-- take database offline/online to associate the pool  
use master  
go  
  
alter database HkDb1 set offline  
go  
alter database HkDb1 set online  
go  
  
USE HkDb1  
go  
  
CREATE TABLE dbo.t1 (  
       c1 int NOT NULL,  
       c2 char(40) NOT NULL,  
       c3 char(8000) NOT NULL,  
  
       CONSTRAINT [pk_t1_c1] PRIMARY KEY NONCLUSTERED HASH (c1) WITH (BUCKET_COUNT = 100000)  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
go  
  
CREATE TABLE dbo.t2 (  
       c1 int NOT NULL,  
       c2 char(40) NOT NULL,  
       c3 char(8000) NOT NULL,  
  
       CONSTRAINT [pk_t2_c1] PRIMARY KEY NONCLUSTERED HASH (c1) WITH (BUCKET_COUNT = 100000)  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
go  
  
CREATE TABLE dbo.t3 (  
       c1 int NOT NULL,  
       c2 char(40) NOT NULL,  
       c3 char(8000) NOT NULL,  
  
       CONSTRAINT [pk_t3_c1] PRIMARY KEY NONCLUSTERED HASH (c1) WITH (BUCKET_COUNT = 1000000)  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
go  
  
-- load 150K rows  
declare @i int = 0  
while (@i <= 150000)  
begin  
       insert t1 values (@i, 'a', replicate ('b', 8000))  
       set @i += 1;  
end  
go  
```  
  
 Quando os dados forem carregados em uma tabela, você poderá consultar as tabelas definidas pelo usuário e a quantidade de armazenamento que eles estão usando. Por exemplo, cada linha de uma tabela pode ter aproximadamente 8070 bytes (o tamanho da alocação é 8.000 (8192 bytes)). Você pode consultar índices por tabela e a quantidade de armazenamento usada pelo índice. Por exemplo, 1 MB representa 100.000 entradas arredondadas para a próxima potência de 2 (2 * * 17) = 131072 de 8 bytes cada um. Uma tabela não pode ter um índice; nesse caso, ela mostrará a alocação de memória do índice. Outras linhas podem representar tabelas do sistema  
  
```  
select convert(char(10), object_name(object_id)) as Name,*   
from sys.dm_db_xtp_table_memory_stats  
```  
  
 Aqui estão as saídas, em duas partes:  
  
```  
Name       object_id   memory_allocated_for_table_kb memory_used_by_table_kb  
---------- ----------- ----------------------------- -----------------------  
t3         629577281   0                             0  
t1         565577053   1372928                       1202351  
t2         597577167   0                             0  
NULL       -6          0                             0  
NULL       -5          0                             0  
NULL       -4          0                             0  
NULL       -3          0                             0  
NULL       -2          192                           25  
  
memory_allocated_for_indexes_kb memory_used_by_indexes_kb  
------------------------------- -------------------------  
8192                            8192  
1024                            1024  
8192                            8192  
2                               2  
24                              24  
2                               2  
2                               2  
16                              16  
```  
  
 A saída de  
  
```  
select  sum(allocated_bytes)/(1024*1024) as total_allocated_MB,   
       sum(used_bytes)/(1024*1024) as total_used_MB  
from sys.dm_db_xtp_memory_consumers  
```  
  
 é  
  
```  
total_allocated_MB   total_used_MB  
-------------------- --------------------  
1357                 1191  
```  
  
 Em seguida, vamos examinar a saída do pool de recursos. Observe que a memória usada pelo pool é 1356 MB  
  
```  
select pool_id,convert(char(10), name) as Name, min_memory_percent, max_memory_percent,   
   max_memory_kb/1024 as max_memory_mb  
from sys.dm_resource_governor_resource_pools  
  
select used_memory_kb/1024 as used_memory_mb ,target_memory_kb/1024 as target_memory_mb  
from sys.dm_resource_governor_resource_pools  
```  
  
 este é o resultado:  
  
```  
pool_id     Name       min_memory_percent max_memory_percent max_memory_mb  
----------- ---------- ------------------ ------------------ --------------------  
1           internal   0                  100                3845  
2           default    0                  100                3845  
259         PoolHkDb1  0                  100                3845  
  
used_memory_mb       target_memory_mb  
-------------------- --------------------  
125                  3845  
32                   3845  
1356                 3845  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de gerenciamento dinâmico de tabela otimizada em memória &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
