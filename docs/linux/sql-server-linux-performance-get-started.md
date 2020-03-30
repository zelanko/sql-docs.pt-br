---
title: Introdução a recursos de desempenho do SQL Server em Linux
description: Este artigo oferece uma introdução dos recursos de desempenho do SQL Server para usuários do Linux que são novos no SQL Server. Muitos desses exemplos funcionam em todas as plataformas, mas o contexto deste artigo é o Linux.
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 60036d26-4797-4872-9a9e-3552841c61be
ms.openlocfilehash: fe60b00654d93c6362a8671318a4b7b88ae90a5f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67896159"
---
# <a name="walkthrough-for-the-performance-features-of-sql-server-on-linux"></a>Passo a passo dos recursos de desempenho do SQL Server em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Se você for um usuário do Linux novo no SQL Server, as tarefas a seguir explicarão alguns dos recursos de desempenho. Elas não são exclusivas nem específicas do Linux, mas ajudam a dar uma ideia de áreas para posterior investigação. Em cada exemplo, um link é fornecido para a documentação detalhada dessa área.

> [!NOTE]
> Os exemplos a seguir usam o banco de dados de exemplo AdventureWorks. Para obter instruções sobre como obter e instalar esse banco de dados de exemplo, confira [Restaurar um banco de dados do SQL Server do Windows para o Linux](sql-server-linux-migrate-restore-database.md).

## <a name="create-a-columnstore-index"></a>Criar um índice columnstore
Um índice columnstore é uma tecnologia para armazenar e consultar grandes armazenamentos de dados em um formato de dados colunar, denominado um columnstore.  

1. Adicione um índice columnstore à tabela SalesOrderDetail executando os seguintes comandos Transact-SQL:

   ```sql
   CREATE NONCLUSTERED COLUMNSTORE INDEX [IX_SalesOrderDetail_ColumnStore]
      ON Sales.SalesOrderDetail
      (UnitPrice, OrderQty, ProductID)
   GO
   ```

2. Execute a consulta a seguir que usa o índice columnstore para examinar a tabela:

   ```sql
   SELECT ProductID, SUM(UnitPrice) SumUnitPrice, AVG(UnitPrice) AvgUnitPrice,
      SUM(OrderQty) SumOrderQty, AVG(OrderQty) AvgOrderQty
   FROM Sales.SalesOrderDetail
      GROUP BY ProductID
      ORDER BY ProductID
   ```

3. Verifique se o índice columnstore foi usado pesquisando a object_id do índice columnstore e confirmando que ele aparece nas estatísticas de uso da tabela SalesOrderDetail:

   ```sql
   SELECT * FROM sys.indexes WHERE name = 'IX_SalesOrderDetail_ColumnStore'
   GO

   SELECT * 
   FROM sys.dm_db_index_usage_stats
      WHERE database_id = DB_ID('AdventureWorks')
      AND object_id = OBJECT_ID('AdventureWorks.Sales.SalesOrderDetail');
   ```
   
## <a name="use-in-memory-oltp"></a>Usar OLTP in-memory
O SQL Server fornece recursos de OLTP in-memory que podem melhorar muito o desempenho de sistemas de aplicativos.  Esta seção do Guia de Avaliação percorrerá as etapas para criar uma tabela com otimização de memória armazenada na memória e um procedimento armazenado compilado nativamente que pode acessar a tabela sem precisar ser compilado ou interpretado.

### <a name="configure-database-for-in-memory-oltp"></a>Configurar banco de dados para OLTP in-memory
1. É recomendável definir o banco de dados para um nível de compatibilidade de pelo menos 130 para usar o OLTP in-memory.  Use a consulta a seguir para verificar o nível de compatibilidade atual do AdventureWorks:  

   ```sql
   USE AdventureWorks
   GO
   SELECT d.compatibility_level
   FROM sys.databases as d
     WHERE d.name = Db_Name();
   GO
   ```
   
   Se necessário, atualize o nível para 130:

   ```sql
   ALTER DATABASE CURRENT
   SET COMPATIBILITY_LEVEL = 130;
   GO
   ```

2. Quando uma transação envolve uma tabela baseada em disco e uma tabela com otimização de memória, é essencial que uma parte com otimização de memória da transação opere no nível de isolamento da transação chamado SNAPSHOT.  Para impor com segurança este nível para as tabelas com otimização de memória em uma transação entre contêineres, execute o seguinte:

   ```sql
   ALTER DATABASE CURRENT SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON
   GO
   ```

3. Antes de poder criar uma tabela com otimização de memória, você precisa criar primeiro um FILEGROUP com otimização de memória e um contêiner para arquivos de dados:

   ```sql
   ALTER DATABASE AdventureWorks ADD FILEGROUP AdventureWorks_mod CONTAINS memory_optimized_data
   GO  
   ALTER DATABASE AdventureWorks ADD FILE (NAME='AdventureWorks_mod', FILENAME='/var/opt/mssql/data/AdventureWorks_mod') TO FILEGROUP AdventureWorks_mod
   GO
   ```

### <a name="create-a-memory-optimized-table"></a>Criar uma tabela com otimização de memória
O armazenamento primário de tabelas com otimização de memória é a memória principal; portanto, diferentemente das tabelas baseadas em disco, os dados não precisam ser lidos do disco para os buffers de memória.  Para criar uma tabela com otimização de memória, use a cláusula MEMORY_OPTIMIZED = ON.

1. Execute a consulta a seguir para criar a tabela com otimização de memória dbo.ShoppingCart.  Como padrão, os dados serão persistentes no disco para fins de durabilidade (observe que DURABILITY também pode ser definido para persistir apenas o esquema). 

   ```sql
   CREATE TABLE dbo.ShoppingCart ( 
   ShoppingCartId INT IDENTITY(1,1) PRIMARY KEY NONCLUSTERED,
   UserId INT NOT NULL INDEX ix_UserId NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000), 
   CreatedDate DATETIME2 NOT NULL, 
   TotalPrice MONEY
   ) WITH (MEMORY_OPTIMIZED=ON) 
   GO
   ```

2. Insira alguns recursos na tabela:

   ```sql
   INSERT dbo.ShoppingCart VALUES (8798, SYSDATETIME(), NULL) 
   INSERT dbo.ShoppingCart VALUES (23, SYSDATETIME(), 45.4) 
   INSERT dbo.ShoppingCart VALUES (80, SYSDATETIME(), NULL) 
   INSERT dbo.ShoppingCart VALUES (342, SYSDATETIME(), 65.4) 
   ```

### <a name="natively-compiled-stored-procedure"></a>Procedimento armazenado nativamente compilado
O SQL Server dá suporte a procedimentos armazenados nativamente compilados que acessam tabelas com otimização de memória. As instruções T-SQL são compiladas no código do computador e armazenadas como DLLs nativas, permitindo um acesso a dados mais rápido e uma execução de consulta mais eficiente do que o T-SQL tradicional.   Os procedimentos armazenados que são marcados com NATIVE_COMPILATION são compilados nativamente. 

1. Execute o script a seguir para criar um procedimento armazenado compilado nativamente que insere um grande número de registros na tabela ShoppingCart:


   ```sql
   CREATE PROCEDURE dbo.usp_InsertSampleCarts @InsertCount int 
    WITH NATIVE_COMPILATION, SCHEMABINDING AS 
   BEGIN ATOMIC 
   WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')

   DECLARE @i int = 0

   WHILE @i < @InsertCount 
    BEGIN 
     INSERT INTO dbo.ShoppingCart VALUES (1, SYSDATETIME() , NULL) 
     SET @i += 1 
    END
   END 
   ```
2. Insira 1 milhão de linhas:

   ```sql
   EXEC usp_InsertSampleCarts 1000000 
   ```

3. Verifique se as linhas foram inseridas:

   ```sql
   SELECT COUNT(*) FROM dbo.ShoppingCart 
   ```

### <a name="learn-more-about-in-memory-oltp"></a>Saiba mais sobre o OLTP in-memory
Para saber mais sobre o OLTP in-memory, confira os seguintes tópicos:

- [Início Rápido 1: tecnologias do OLTP in-memory para um desempenho mais rápido do Transact-SQL](../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md)
- [Migrando para OLTP na memória](../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)
- [Tabela temporária e variável de tabela mais rápidas usando a otimização de memória](../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)
- [Monitorar e solucionar problemas de uso da memória](../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md)
- [OLTP na memória (otimização na memória)](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)

## <a name="use-query-store"></a>Usar o Repositório de Consultas
O Repositório de Consultas coleta informações de desempenho detalhadas sobre consultas, planos de execução e estatísticas de runtime.

O Repositório de Consultas não está ativo por padrão e pode ser habilitado com ALTER DATABASE:

   ```sql
   ALTER DATABASE AdventureWorks SET QUERY_STORE = ON;
   ```

Execute a consulta a seguir para retornar informações sobre consultas e planos no repositório de consultas: 

   ```sql
   SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*
   FROM sys.query_store_plan AS Pl
      JOIN sys.query_store_query AS Qry
         ON Pl.query_id = Qry.query_id
      JOIN sys.query_store_query_text AS Txt
         ON Qry.query_text_id = Txt.query_text_id ;
   ```

## <a name="query-dynamic-management-views"></a>Consultar exibições de gerenciamento dinâmico
As exibições de gerenciamento dinâmico retornam informações do estado do servidor que podem ser usadas para monitorar a integridade de uma instância do servidor, diagnosticar problemas e ajustar o desempenho.

Para consultar a exibição de gerenciamento dinâmico de estatísticas dm_os_wait:

   ```sql
   SELECT wait_type, wait_time_ms
   FROM sys.dm_os_wait_stats;
   ```
