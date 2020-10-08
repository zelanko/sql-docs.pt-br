---
title: Padrão de aplicativo – particionamento de tabelas com otimização de memória
description: Saiba mais sobre o padrão de design de aplicativo OLTP in-memory que armazena dados ativos atuais em uma tabela com otimização de memória e dados mais antigos em uma tabela particionada.
ms.custom: seo-dt-2019,issue-PR=4700-14820
ms.date: 05/03/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 3f867763-a8e6-413a-b015-20e9672cc4d1
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 08fb58f77382dae2d6455cc181c983798c89050a
ms.sourcegitcommit: d56a834269132a83e5fe0a05b033936776cda8bb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91529407"
---
# <a name="application-pattern-for-partitioning-memory-optimized-tables"></a>Padrão de aplicativo para particionamento de tabelas com otimização de memória

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

[!INCLUDE[hek_2](../../includes/hek-2-md.md)] é compatível com um padrão de design de aplicativo repleto de recursos de desempenho em dados relativamente atuais. Esse padrão pode ser aplicado quando os dados atuais são lidos ou atualizados com muito mais frequência do que os dados mais antigos. Nesse caso, dizemos que os dados atuais estão *ativos* ou *quentes* e os dados mais antigos estão *frios*.

A principal ideia é armazenar dados *de acesso frequente* em uma tabela com otimização de memória. Semanal ou mensalmente, os dados mais antigos que se tornaram *frios* são movidos para uma tabela particionada. A tabela particionada tem seus dados armazenados em um disco ou em outro disco rígido, não na memória.

Normalmente, esse design usa uma chave **datetime** para permitir que o processo de movimentação diferencie com eficiência os dados de acesso quentes e os frios.

## <a name="advanced-partitioning"></a>Particionamento avançado

O design pretende imitar a existência de uma tabela particionada que também tenha uma partição com otimização de memória. Para que esse design funcione, você deve garantir que todas as tabelas compartilhem um esquema comum. O exemplo de código mais adiante neste artigo mostra a técnica.

Presumimos que novos dados sejam quentes por definição. Os dados de acesso frequente são inseridos e atualizados na tabela com otimização de memória. Os dados frios são mantidos na tabela particionada tradicional. Periodicamente, um procedimento armazenado adiciona uma nova partição. A partição contém os dados frios mais recentes que foram movidos para fora da tabela com otimização de memória.

Se uma operação precisar apenas de dados de acesso frequente, ela poderá usar procedimentos armazenados compilados nativamente para acessar os dados. As operações que podem acessar dados quentes ou frios devem usar o [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado para unir a tabela com otimização de memória com a tabela particionada.

### <a name="add-a-partition"></a>Adicionar uma partição

Os dados que se tornaram frios recentemente devem ser movidos para a tabela particionada. As etapas para essa troca de partição periódica são as seguintes:

1. Para os dados na tabela com otimização de memória, determine a data e hora de limite ou corte entre os dados quentes e aqueles que acabaram de ficar frios.
2. Insira os dados que acabaram de ficar frios da tabela OLTP in-memory em uma tabela de *preparo\_frio*.
3. Exclua os mesmos dados frios da tabela com otimização de memória.
4. Troque a tabela de preparo\_frio em uma partição.
5. Adicione a partição.

#### <a name="maintenance-window"></a>Janela de manutenção

Uma das etapas anteriores é excluir os dados que acabaram de ficar frios da tabela com otimização de memória. Há um intervalo de tempo entre essa exclusão e a etapa final que adiciona a nova partição. Durante esse intervalo, qualquer aplicativo que tente ler os dados que acabaram de ficar frios novos falhará.

Para ver um exemplo relacionado, veja [Particionamento no nível de aplicativo](../../relational-databases/in-memory-oltp/application-level-partitioning.md).

## <a name="code-sample"></a>Exemplo de código

O exemplo do Transact-SQL a seguir é exibido em uma série de blocos de código menores apenas para facilitar a apresentação. Você poderia acrescentá-los a um grande bloco de código para seu teste.

Como um todo, o exemplo de T-SQL mostra como usar uma tabela com otimização de memória com uma tabela baseada em disco particionada.

As primeiras fases do exemplo de T-SQL criam o banco de dados e, em seguida, criam objetos como tabelas no banco de dados. As fases posteriores mostram como mover dados de uma tabela com otimização de memória para uma tabela particionada.

### <a name="create-a-database"></a>Criar um banco de dados

Esta seção do exemplo de T-SQL cria um banco de dados de teste. O banco de dados está configurado para dar suporte a tabelas com otimização de memória e tabelas particionadas.

```sql
CREATE DATABASE PartitionSample;
GO

-- Add a FileGroup, enabled for In-Memory OLTP.
-- Change file path as needed.

ALTER DATABASE PartitionSample
    ADD FILEGROUP PartitionSample_mod
    CONTAINS MEMORY_OPTIMIZED_DATA;

ALTER DATABASE PartitionSample
    ADD FILE(
        NAME = 'PartitionSample_mod',
        FILENAME = 'c:\data\PartitionSample_mod')
    TO FILEGROUP PartitionSample_mod;
GO
```

### <a name="create-a-memory-optimized-table-for-hot-data"></a>Criar uma tabela com otimização de memória para dados de acesso frequente

Esta seção cria a tabela com otimização de memória que contém os dados mais recentes, que, na maioria dos casos, ainda são dados de acesso frequente.

```sql
USE PartitionSample;
GO

-- Create a memory-optimized table for the HOT Sales Order data.
-- Notice the index that uses datetime2.

CREATE TABLE dbo.SalesOrders_hot (
   so_id INT IDENTITY PRIMARY KEY NONCLUSTERED,
   cust_id INT NOT NULL,
   so_date DATETIME2 NOT NULL INDEX ix_date NONCLUSTERED,
   so_total MONEY NOT NULL,
   INDEX ix_date_total NONCLUSTERED (so_date desc, so_total desc)
) WITH (MEMORY_OPTIMIZED=ON);
GO
```

### <a name="create-a-partitioned-table-for-cold-data"></a>Criar uma tabela particionada para dados frios

Esta seção cria a tabela particionada que contém os dados frios.

```sql
-- Create a partition and table for the COLD Sales Order data.
-- Notice the index that uses datetime2.

CREATE PARTITION FUNCTION [ByDatePF](datetime2) AS RANGE RIGHT
   FOR VALUES();
GO

CREATE PARTITION SCHEME [ByDateRange]
   AS PARTITION [ByDatePF]
   ALL TO ([PRIMARY]);
GO

CREATE TABLE dbo.SalesOrders_cold (
   so_id INT NOT NULL,
   cust_id INT NOT NULL,
   so_date DATETIME2 NOT NULL,
   so_total MONEY NOT NULL,
   CONSTRAINT PK_SalesOrders_cold PRIMARY KEY (so_id, so_date),
   INDEX ix_date_total NONCLUSTERED (so_date desc, so_total desc)
) ON [ByDateRange](so_date);
GO
```

### <a name="create-a-table-to-store-cold-data-during-move"></a>Criar uma tabela para armazenar dados frios durante a movimentação

Esta seção cria a tabela de preparo\_frio. Também é criada uma exibição que une os dados quentes e frios das duas tabelas.

```sql
-- A table used to briefly stage the newly cold data, during moves to a partition.

CREATE TABLE dbo.SalesOrders_cold_staging (
   so_id INT NOT NULL,
   cust_id INT NOT NULL,
   so_date datetime2 NOT NULL,
   so_total MONEY NOT NULL,
   CONSTRAINT PK_SalesOrders_cold_staging PRIMARY KEY (so_id, so_date),
   INDEX ix_date_total NONCLUSTERED (so_date desc, so_total desc),
   CONSTRAINT CHK_SalesOrders_cold_staging CHECK (so_date >= '1900-01-01')
);
GO

-- A view, for retrieving the aggregation of hot plus cold data.

CREATE VIEW dbo.SalesOrders
AS SELECT so_id,
          cust_id,
          so_date,
          so_total,
          1 AS 'is_hot'
       FROM dbo.SalesOrders_hot
   UNION ALL
   SELECT so_id,
          cust_id,
          so_date,
          so_total,
          0 AS 'is_cold'
       FROM dbo.SalesOrders_cold;
GO
```

### <a name="create-the-stored-procedure"></a>Criar o procedimento armazenado

Esta seção cria o procedimento armazenado que você executa periodicamente. O procedimento move dados que acabaram de ficar frios da tabela com otimização de memória para a tabela particionada.

```sql
-- A stored procedure to move all newly cold sales orders data
-- to its staging location.

CREATE PROCEDURE dbo.usp_SalesOrdersOffloadToCold @splitdate datetime2
   AS
   BEGIN
      BEGIN TRANSACTION;

      -- Insert the cold data as a temporary heap.
      INSERT INTO dbo.SalesOrders_cold_staging WITH (TABLOCKX)
      SELECT so_id , cust_id , so_date , so_total
         FROM dbo.SalesOrders_hot WITH (serializable)
         WHERE so_date <= @splitdate;

      -- Delete the moved data from the hot table.
      DELETE FROM dbo.SalesOrders_hot WITH (SERIALIZABLE)
         WHERE so_date <= @splitdate;

      -- Update the partition function, and switch in the new partition.
      ALTER PARTITION SCHEME [ByDateRange] NEXT USED [PRIMARY];

      DECLARE @p INT = (
        SELECT MAX(partition_number)
            FROM sys.partitions
            WHERE object_id = OBJECT_ID('dbo.SalesOrders_cold'));

      EXEC sp_executesql
        N'ALTER TABLE dbo.SalesOrders_cold_staging
            SWITCH TO dbo.SalesOrders_cold partition @i',
        N'@i int',
        @i = @p;

      ALTER PARTITION FUNCTION [ByDatePF]()
      SPLIT RANGE( @splitdate);

      -- Modify a constraint on the cold_staging table, to align with new partition.
      ALTER TABLE dbo.SalesOrders_cold_staging
         DROP CONSTRAINT CHK_SalesOrders_cold_staging;

      DECLARE @s nvarchar( 100) = CONVERT( nvarchar( 100) , @splitdate , 121);
      DECLARE @sql nvarchar( 1000) = N'alter table dbo.SalesOrders_cold_staging 
         add constraint CHK_SalesOrders_cold_staging check (so_date > ''' + @s + ''')';
      PRINT @sql;
      EXEC sp_executesql @sql;

      COMMIT;
END;
GO
```

### <a name="prepare-sample-data-and-demo-the-stored-procedure"></a>Preparar dados de exemplo e demonstrar o procedimento armazenado

Esta seção gera e insere dados de exemplo e, em seguida, executa o procedimento armazenado como uma demonstração.

```sql
-- Insert sample values into the hot table.
INSERT INTO dbo.SalesOrders_hot VALUES(1,SYSDATETIME(), 1);
GO
INSERT INTO dbo.SalesOrders_hot VALUES(1, SYSDATETIME(), 1);
GO
INSERT INTO dbo.SalesOrders_hot VALUES(1, SYSDATETIME(), 1);
GO

-- Verify that the hot data is in the table, by selecting from the view.
SELECT * FROM dbo.SalesOrders;
GO

-- Treat all data in the hot table as cold data:
-- Run the stored procedure, to move (offload) all sales orders to date to cold storage.
DECLARE @t datetime2 = SYSDATETIME();
EXEC dbo.usp_SalesOrdersOffloadToCold @t;

-- Again, read hot plus cold data from the view.
SELECT * FROM dbo.SalesOrders;
GO

-- Retrieve the name of every partition.
SELECT OBJECT_NAME( object_id) , * FROM sys.dm_db_partition_stats ps
   WHERE object_id = OBJECT_ID( 'dbo.SalesOrders_cold');

-- Insert more data into the hot table.
INSERT INTO dbo.SalesOrders_hot VALUES(2, SYSDATETIME(), 1);
GO
INSERT INTO dbo.SalesOrders_hot VALUES(2, SYSDATETIME(), 1);
GO
INSERT INTO dbo.SalesOrders_hot VALUES(2, SYSDATETIME(), 1);
GO

-- Read hot plus cold data from the view.
SELECT * FROM dbo.SalesOrders;
GO

-- Again, run the stored procedure, to move all sales orders to date to cold storage.
DECLARE @t datetime2 = SYSDATETIME();
EXEC dbo.usp_SalesOrdersOffloadToCold @t;

-- Read hot plus cold data from the view.
SELECT * FROM dbo.SalesOrders;
GO

-- Again, retrieve the name of every partition.
-- The stored procedure can modify the partitions.
SELECT OBJECT_NAME( object_id) , partition_number , row_count
  FROM sys.dm_db_partition_stats ps
  WHERE object_id = OBJECT_ID( 'dbo.SalesOrders_cold')
    AND index_id = 1;
```

### <a name="drop-all-the-demo-objects"></a>Remover todos os objetos de demonstração

Lembre-se de limpar o banco de dados de teste de demonstração de seu sistema de teste.

```sql
-- You must first leave the context of the PartitionSample database.

-- USE <A-Database-Name-Here>;
GO

DROP DATABASE PartitionSample;
GO
```

## <a name="see-also"></a>Consulte Também

[Memory-Optimized Tables](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)
