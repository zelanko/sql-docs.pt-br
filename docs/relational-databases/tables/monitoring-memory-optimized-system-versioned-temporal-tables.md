---
description: Monitorando tabelas temporais com controle da versão do sistema com otimização de memória
title: Monitorando tabelas temporais com controle de versão do sistema e otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 7a06785d-dbcb-44de-b95c-26b131471bee
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 386a4d1f3119744244d71a22355be643531a0b56
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646407"
---
# <a name="monitoring-memory-optimized-system-versioned-temporal-tables"></a>Monitorando tabelas temporais com controle da versão do sistema com otimização de memória


[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]


Você pode usar modos de exibição existentes para controlar o consumo de memória resumido e detalhado para cada tabela com controle da versão do sistema com otimização de memória.

Consumo de memória detalhado (dividir por tabela de preparo de histórico interno e com controle da versão do sistema principal):

```sql
--Details of memory consumption
WITH InMemoryTemporalTables
AS
   (
      SELECT SCHEMA_NAME ( T1.schema_id ) AS TemporalTableSchema
         , T1.object_id AS TemporalTableObjectId
         , IT.object_id AS InternalTableObjectId
         , OBJECT_NAME ( IT.parent_object_id ) AS TemporalTableName
         , IT.Name AS InternalHistoryStagingName
      FROM sys.internal_tables IT
      JOIN sys.tables T1 ON IT.parent_object_id = T1.object_id
      WHERE T1.is_memory_optimized = 1 AND T1.temporal_type = 2
   )
SELECT
   TemporalTableSchema
   , T.TemporalTableName
   , T.InternalHistoryStagingName,
      CASE
         WHEN C.object_id = T.TemporalTableObjectId
         THEN 'Temporal Table Consumption'
         ELSE 'Internal Table Consumption'
         END ConsumedBy
   , C.*
FROM sys.dm_db_xtp_memory_consumers C
JOIN InMemoryTemporalTables T
   ON C.object_id = T.TemporalTableObjectId OR C.object_id = T.InternalTableObjectId
   WHERE T.TemporalTableSchema = 'dbo' AND T.TemporalTableName = 'FXCurrencyPairs'
;
```

Resumo de consumo de memória (total para uma tabela com memória otimizada com controle da versão do sistema):

```sql
--Summary of memory consumption
WITH InMemoryTemporalTables
AS
   (
      SELECT SCHEMA_NAME ( T1.schema_id ) AS TemporalTableSchema
         , T1.object_id AS TemporalTableObjectId
         , IT.object_id AS InternalTableObjectId
         , OBJECT_NAME ( IT.parent_object_id ) AS TemporalTableName
         , IT.Name AS InternalHistoryStagingName
      FROM sys.internal_tables IT
      JOIN sys.tables T1 ON IT.parent_object_id = T1.object_id
      WHERE T1.is_memory_optimized = 1 AND T1.temporal_type = 2
   )
, DetailedConsumption
AS
(
   SELECT TemporalTableSchema
      , T.TemporalTableName
      , T.InternalHistoryStagingName
      , CASE
         WHEN C.object_id = T.TemporalTableObjectId
         THEN 'Temporal Table Consumption'
         ELSE 'Internal Table Consumption'
         END ConsumedBy
      , C.*
   FROM sys.dm_db_xtp_memory_consumers C
   JOIN InMemoryTemporalTables T
   ON C.object_id = T.TemporalTableObjectId OR C.object_id = T.InternalTableObjectId
)
SELECT TemporalTableSchema
   TemporalTableName
   , sum ( allocated_bytes ) AS allocated_bytes
   , sum ( used_bytes ) AS used_bytes
FROM DetailedConsumption
WHERE TemporalTableSchema = 'dbo' ANDTemporalTableName = 'FXCurrencyPairs'
GROUP BY TemporalTableSchema, TemporalTableName
;
```

## <a name="see-also"></a>Consulte Também

- [Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [Criação de uma tabela temporal com controle da versão do sistema com otimização de memória](../../relational-databases/tables/creating-a-memory-optimized-system-versioned-temporal-table.md)
- [Trabalhando com tabelas temporais com controle da versão do sistema e otimização de memória](../../relational-databases/tables/working-with-memory-optimized-system-versioned-temporal-tables.md)
- [Considerações sobre desempenho com tabelas temporais com versão do sistema e otimização de memória](../../relational-databases/tables/memory-optimized-system-versioned-temporal-tables-performance.md)
- [Tabelas temporais](../../relational-databases/tables/temporal-tables.md)
- [Verificações de consistência do sistema de tabela temporal](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [Gerenciar a retenção de dados históricos em tabelas temporais com controle de versão do sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [Funções e exibições de metadados de tabela temporal](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)
