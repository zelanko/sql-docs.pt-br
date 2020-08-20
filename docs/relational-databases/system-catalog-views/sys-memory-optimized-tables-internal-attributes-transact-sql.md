---
description: sys.memory_optimized_tables_internal_attributes (Transact-SQL)
title: sys. memory_optimized_tables_internal_attributes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.memory_optimized_tables_internal_attributes
- sys.memory_optimized_tables_internal_attributes_TSQL
- memory_optimized_tables_internal_attributes
- memory_optimized_tables_internal_attributes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.memory_optimized_tables_internal_attributes catalog view
ms.assetid: 78ef5807-0504-4de8-9a01-ede6c03c7ff1
author: jodebrui
ms.author: jodebrui
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fc11ec8d075d52643f06eb91f0a55a1b6948c88c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455232"
---
# <a name="sysmemory_optimized_tables_internal_attributes-transact-sql"></a>sys.memory_optimized_tables_internal_attributes (Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

Contém uma linha para cada tabela com otimização de memória interna usada para armazenar as tabelas com otimização de memória do usuário. Cada tabela de usuário corresponde a uma ou mais tabelas internas. Uma única tabela é usada para o armazenamento dos principais dados. Tabelas internas adicionais são usadas para dar suporte a recursos como temporal, índice columnstore e armazenamento fora de linha (LOB) para tabelas com otimização de memória.
 
| Nome da coluna  | Tipo de dados  | Descrição |
| :------ |:----------| :-----|
|object_id  |**int**|       ID da tabela de usuário. Tabelas internas com otimização de memória que existem para dar suporte a uma tabela de usuário (como armazenamento fora de linha ou linhas excluídas no caso de combinações de Hk/Columnstore) têm o mesmo object_id como pai. |
|xtp_object_id  |**bigint**|    ID de objeto OLTP in-memory correspondente à tabela interna com otimização de memória usada para dar suporte à tabela de usuário. Ela é exclusiva no banco de dados e pode mudar com o tempo de vida do objeto. 
|type|  **int** |   Tipo de tabela interna.<br/><br/> 0 => DELETED_ROWS_TABLE <br/> 1 => USER_TABLE <br/> 2 => DICTIONARIES_TABLE<br/>3 => SEGMENTS_TABLE<br/>4 => ROW_GROUPS_INFO_TABLE<br/>5 => INTERNAL OFF-ROW DATA TABLE<br/>252 => INTERNAL_TEMPORAL_HISTORY_TABLE | 
|type_desc| **nvarchar(60)**|   Descrição do tipo<br/><br/>DELETED_ROWS_TABLE -> Linhas de acompanhamento de tabela interna excluídas de um índice columnstore<br/>USER_TABLE -> Tabela contendo os dados do usuário em linha<br/>DICTIONARIES_TABLE -> Dicionários para um índice columnstore<br/>SEGMENTS_TABLE -> Segmentos compactados para um índice columnstore<br/>ROW_GROUPS_INFO_TABLE -> Metadados sobre grupos de linhas compactados de um índice columnstore<br/>INTERNAL OFF-ROW DATA TABLE -> Tabela interna usada para o armazenamento de uma coluna fora da linha. Nesse caso, minor_id reflete column_id.<br/>INTERNAL_TEMPORAL_HISTORY_TABLE -> Parte final mais acessada da tabela de histórico baseada em disco. Linhas inseridas no histórico de linhas são inseridas primeiro nessa tabela interna com otimização de memória. Há uma tarefa em segundo plano que move as linhas de forma assíncrona desta tabela interna para a tabela de histórico baseada em disco. |
|minor_id|  **int**|    0 indica um usuário ou uma tabela interna<br/><br/>Não 0 indica a ID de uma coluna armazenada fora de linha. Junções com column_id em sys.columns.<br/><br/>Cada coluna armazenada fora de linha tem uma linha correspondente nesta exibição do sistema.|

## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-all-columns-that-are-stored-off-row"></a>a. Retornando todas as colunas armazenadas fora de linha

O seguinte script T-SQL ilustra uma tabela com várias colunas LOB não grandes e uma única coluna LOB:

```Transact-SQL
CREATE TABLE dbo.LargeTableSample
(
      Id   int IDENTITY PRIMARY KEY NONCLUSTERED,
      C1   nvarchar(4000),
      C2   nvarchar(4000),
      C3   nvarchar(4000),
      C4   nvarchar(4000),
      Misc nvarchar(max)
) WITH (MEMORY_OPTIMIZED = ON);
GO
```

A consulta a seguir mostra todas as colunas que são armazenadas fora da linha, juntamente com seus tamanhos. Um tamanho de -1 indica uma coluna LOB. Todas as colunas LOB são armazenadas fora de linha.

```Transact-SQL
SELECT 
  QUOTENAME(SCHEMA_NAME(o.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(moa.object_id)) AS 'table', 
  c.name AS 'column', 
  c.max_length
FROM sys.memory_optimized_tables_internal_attributes moa
     JOIN sys.columns c ON moa.object_id = c.object_id AND moa.minor_id=c.column_id
     JOIN sys.objects o on moa.object_id=o.object_id 
WHERE moa.type=5;
```

### <a name="b-returning-memory-consumption-of-all-columns-that-are-stored-off-row"></a>B. Retornando o consumo de memória de todas as colunas armazenados fora de linha

Para obter mais detalhes sobre o consumo de memória de colunas fora de linha, você pode usar a seguinte consulta, que mostra o consumo de memória de todas as tabelas internas e seus índices usados para armazenar as colunas fora de linha:

```Transact-SQL
SELECT
  QUOTENAME(SCHEMA_NAME(o.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(moa.object_id)) AS 'table',
  c.name AS 'column',
  c.max_length,
  mc.memory_consumer_desc,
  mc.index_id,
  mc.allocated_bytes,
  mc.used_bytes
FROM sys.memory_optimized_tables_internal_attributes moa
   JOIN sys.columns c ON moa.object_id = c.object_id AND moa.minor_id=c.column_id
   JOIN sys.dm_db_xtp_memory_consumers mc ON moa.xtp_object_id=mc.xtp_object_id
   JOIN sys.objects o on moa.object_id=o.object_id 
WHERE moa.type=5;
```

### <a name="c-returning-memory-consumption-of-columnstore-indexes-on-memory-optimized-tables"></a>C. Retornando o consumo de memória de índices columnstore em tabelas com otimização de memória

Use a consulta a seguir para mostrar o consumo de memória de índices columnstore em tabelas com otimização de memória:

```Transact-SQL
SELECT
  QUOTENAME(SCHEMA_NAME(o.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(moa.object_id)) AS 'table',
  i.name AS 'columnstore index',
  SUM(mc.allocated_bytes) / 1024 as [allocated_kb],
  SUM(mc.used_bytes) / 1024 as [used_kb]
FROM sys.memory_optimized_tables_internal_attributes moa
   JOIN sys.indexes i ON moa.object_id = i.object_id AND i.type in (5,6)
   JOIN sys.dm_db_xtp_memory_consumers mc ON moa.xtp_object_id=mc.xtp_object_id
   JOIN sys.objects o on moa.object_id=o.object_id
WHERE moa.type IN (0, 2, 3, 4)
GROUP BY o.schema_id, moa.object_id, i.name;
```

Use a seguinte consulta dividir o consumo de memória entre estruturas internas usadas para índices columnstore em tabelas com otimização de memória:

```Transact-SQL
SELECT
  QUOTENAME(SCHEMA_NAME(o.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(moa.object_id)) AS 'table',
  i.name AS 'columnstore index',
  moa.type_desc AS 'internal table',
  mc.index_id AS 'index',
  mc.memory_consumer_desc,
  mc.allocated_bytes / 1024 as [allocated_kb],
  mc.used_bytes / 1024 as [used_kb]
FROM sys.memory_optimized_tables_internal_attributes moa
   JOIN sys.indexes i ON moa.object_id = i.object_id AND i.type in (5,6)
   JOIN sys.dm_db_xtp_memory_consumers mc ON moa.xtp_object_id=mc.xtp_object_id
   JOIN sys.objects o on moa.object_id=o.object_id
WHERE moa.type IN (0, 2, 3, 4)
```


