---
title: Padrão de aplicativo para particionamento de tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 3f867763-a8e6-413a-b015-20e9672cc4d1
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 68000dfa707e7cba16717f8bc9310c6db4b927bb
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65095951"
---
# <a name="application-pattern-for-partitioning-memory-optimized-tables"></a>Padrão de aplicativo para particionamento de tabelas com otimização de memória
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[hek_2](../../includes/hek-2-md.md)] dá suporte a um padrão em que um valor limitado de dados ativos é mantido em uma tabela com otimização de memória, enquanto os dados acessados com menos frequência são processados no disco. Geralmente, esse seria um cenário onde os dados são armazenados com base em uma chave **datetime** .  
  
 Você pode emular tabelas particionadas usando tabelas com otimização de memória mantendo uma tabela particionada e uma tabela com otimização de memória com um esquema comum. Os dados atuais seriam inseridos e atualizados na tabela com otimização de memória, enquanto os dados acessados com menos frequência seriam mantidos na tabela particionada tradicional.  
  
 Um aplicativo que sabe que há dados ativos em uma tabela com otimização de memória pode usar procedimentos armazenados compilados nativamente para acessar os dados. As operações que precisam acessar o período inteiro de dados, ou que talvez não saibam qual tabela mantém dados relevantes, usam o [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado para unir a tabela com otimização de memória à tabela particionada.  
  
 Essa alternância de partição é descrita como se segue:  
  
-   Insira dados da tabela OLTP na memória em uma tabela de preparo, possivelmente usando uma data de corte.  
  
-   Exclua os mesmos dados da tabela com otimização de memória.  
  
-   Faça trocas na tabela de preparo.  
  
-   Adicione a partição ativa.  
  
 ![Partition switch.](../../relational-databases/in-memory-oltp/media/hekaton-partitioned-tables.gif "Partition switch.")  
Manutenção de dados ativos  
  
 As ações que começam com Excluir Ordens Ativas precisam ser executadas durante uma janela de manutenção para evitar consultas com dados ausentes durante o tempo entre a exclusão de dados e a alternância na tabela de preparo.  
  
 Para ver um exemplo relacionado, veja [Particionamento no nível de aplicativo](../../relational-databases/in-memory-oltp/application-level-partitioning.md).  
  
## <a name="code-sample"></a>Exemplo de código  
 O exemplo a seguir mostra como usar uma tabela com otimização de memória com uma tabela baseada em disco particionada. Os dados mais usados são armazenados na memória. Para salvar os dados em disco, criar uma nova partição e copie os dados para a tabela particionada.  
  
 A primeira parte deste exemplo cria o banco de dados e os objetos necessários. A segunda parte do exemplo mostra como mover dados de uma tabela com otimização de memória em uma tabela particionada.  
  
```sql  
CREATE DATABASE partitionsample;  
GO  
  
-- enable for In-Memory OLTP - change file path as needed  
ALTER DATABASE partitionsample
    ADD FILEGROUP partitionsample_mod
    CONTAINS MEMORY_OPTIMIZED_DATA;

ALTER DATABASE partitionsample
    ADD FILE(
        NAME = 'partitionsample_mod',
        FILENAME = 'c:\data\partitionsample_mod')
    TO FILEGROUP partitionsample_mod;  
GO  
  
USE partitionsample;  
GO  
  
-- frequently used portion of the SalesOrders - memory-optimized  
  
CREATE TABLE dbo.SalesOrders_hot (  
   so_id INT IDENTITY PRIMARY KEY NONCLUSTERED,  
   cust_id INT NOT NULL,  
   so_date DATETIME2 NOT NULL INDEX ix_date NONCLUSTERED,  
   so_total MONEY NOT NULL,  
   INDEX ix_date_total NONCLUSTERED (so_date desc, so_total desc)  
) WITH (MEMORY_OPTIMIZED=ON)  
GO  
  
-- cold portion of the SalesOrders - partitioned disk-based table  
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
) ON [ByDateRange](so_date)  
GO  
  
-- table for temporary partitions  
CREATE TABLE dbo.SalesOrders_cold_staging (  
   so_id INT NOT NULL,  
   cust_id INT NOT NULL,  
   so_date datetime2 NOT NULL,  
   so_total MONEY NOT NULL,  
   CONSTRAINT PK_SalesOrders_cold_staging PRIMARY KEY (so_id, so_date),  
   INDEX ix_date_total NONCLUSTERED (so_date desc, so_total desc),  
   CONSTRAINT CHK_SalesOrders_cold_staging CHECK (so_date >= '1900-01-01')  
)  
GO  
  
-- aggregate view of the hot and cold data  
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
          0 AS 'is_hot'  
       FROM dbo.SalesOrders_cold;  
GO  
  
-- move all sales orders up to the split date to cold storage  
CREATE PROCEDURE dbo.usp_SalesOrdersOffloadToCold @splitdate datetime2  
   AS  
   BEGIN  
      BEGIN TRANSACTION;  
      -- create new heap based on the hot data to be moved to cold storage  
      INSERT INTO dbo.SalesOrders_cold_staging WITH( TABLOCKX)  
      SELECT so_id , cust_id , so_date , so_total  
         FROM dbo.SalesOrders_hot WITH ( serializable)  
         WHERE so_date <= @splitdate;  
  
      -- remove moved data  
      DELETE FROM dbo.SalesOrders_hot WITH( SERIALIZABLE)  
         WHERE so_date <= @splitdate;  
  
      -- update partition function, and switch in new partition  
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
  
      -- modify constraint on staging table to align with new partition  
      ALTER TABLE dbo.SalesOrders_cold_staging DROP CONSTRAINT CHK_SalesOrders_cold_staging;  
  
      DECLARE @s nvarchar( 100) = CONVERT( nvarchar( 100) , @splitdate , 121);  
      DECLARE @sql nvarchar( 1000) = N'alter table dbo.SalesOrders_cold_staging   
         add constraint CHK_SalesOrders_cold_staging check (so_date > ''' + @s + ''')';  
      PRINT @sql;  
      EXEC sp_executesql @sql;  
  
      COMMIT;  
END;  
GO  
  
-- insert sample values in the hot table  
INSERT INTO dbo.SalesOrders_hot VALUES(1,SYSDATETIME(), 1);   
GO  
  
INSERT INTO dbo.SalesOrders_hot VALUES(1, SYSDATETIME(), 1);  
GO  
  
INSERT INTO dbo.SalesOrders_hot VALUES(1, SYSDATETIME(), 1);  
GO  
  
-- verify contents of the table  
SELECT *  FROM dbo.SalesOrders;  
GO  
  
-- offload all sales orders to date to cold storage  
DECLARE  @t datetime2 = SYSDATETIME();  
EXEC dbo.usp_SalesOrdersOffloadToCold @t;  
  
-- verify contents of the tables  
SELECT * FROM dbo.SalesOrders;  
GO  
  
-- verify partitions  
SELECT OBJECT_NAME( object_id) , * FROM sys.dm_db_partition_stats ps  
   WHERE object_id = OBJECT_ID( 'dbo.SalesOrders_cold');  
  
-- insert more rows in the hot table  
INSERT INTO dbo.SalesOrders_hot VALUES(2, SYSDATETIME(), 1);  
GO  
  
INSERT INTO dbo.SalesOrders_hot VALUES(2, SYSDATETIME(), 1);  
GO  
  
INSERT INTO dbo.SalesOrders_hot VALUES(2, SYSDATETIME(), 1);  
GO  
  
-- verify contents of the tables  
SELECT * FROM dbo.SalesOrders;  
GO  
  
-- offload all sales orders to date to cold storage  
DECLARE @t datetime2 = SYSDATETIME();  
EXEC dbo.usp_SalesOrdersOffloadToCold @t;  
  
-- verify contents of the tables  
SELECT * FROM dbo.SalesOrders;  
GO  
  
-- verify partitions  
SELECT OBJECT_NAME( object_id) , partition_number , row_count  FROM sys.dm_db_partition_stats ps  
  WHERE object_id = OBJECT_ID( 'dbo.SalesOrders_cold') AND index_id = 1;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas com otimização de memória](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  
