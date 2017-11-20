---
title: "Começar com recursos de desempenho do SQL Server no Linux | Microsoft Docs"
description: "Este tópico fornece uma introdução dos recursos de desempenho do SQL Server para os usuários do Linux que são novos para o SQL Server. Muitos desses exemplos funcionam em todas as plataformas, mas o contexto deste artigo é Linux."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.technology: database-engine
ms.assetid: 60036d26-4797-4872-9a9e-3552841c61be
ms.custom: 
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 5936634cf243216f5916812bbe5ec04767932ec7
ms.contentlocale: pt-br
ms.lasthandoff: 09/27/2017

---
# <a name="walkthrough-for-the-performance-features-of-sql-server-on-linux"></a>Instruções passo a passo para os recursos de desempenho do SQL Server no Linux

Se você for um usuário do Linux que há de novo para o SQL Server, as tarefas a seguir mostram alguns dos recursos de desempenho. Eles não são exclusivas ou específicas para o Linux, mas ajuda a dar uma ideia de áreas para investigar mais. Em cada exemplo é fornecido um link para a documentação de profundidade para a área.

> [!NOTE]
> Os exemplos a seguir usam o banco de dados de exemplo AdventureWorks. Para obter instruções sobre como obter e instalar esse banco de dados de exemplo, consulte [restaurar um banco de dados do SQL Server do Windows para Linux](sql-server-linux-migrate-restore-database.md).

## <a name="create-a-columnstore-index"></a>Criar um índice Columnstore
Um índice columnstore é uma tecnologia para armazenar e consultar grandes armazenamentos de dados em um formato de dados Colunar, chamado columnstore.  

1. Adicione um índice Columnstore na tabela SalesOrderDetail executando o T-SQL a seguir:

   ```sql
   CREATE NONCLUSTERED COLUMNSTORE INDEX [IX_SalesOrderDetail_ColumnStore]
      ON Sales.SalesOrderDetail
      (UnitPrice, OrderQty, ProductID)
   GO
   ```

2. Execute a consulta a seguir que usará o índice Columnstore para digitalizar a tabela:

   ```sql
   SELECT ProductID, SUM(UnitPrice) SumUnitPrice, AVG(UnitPrice) AvgUnitPrice,
      SUM(OrderQty) SumOrderQty, AVG(OrderQty) AvgOrderQty
   FROM Sales.SalesOrderDetail
      GROUP BY ProductID
      ORDER BY ProductID
   ```

3. Verifique se o índice Columnstore foi usado por pesquisar object_id para o índice Columnstore e confirmando se ele é exibido nas estatísticas de uso para a tabela SalesOrderDetail:

   ```sql
   SELECT * FROM sys.indexes WHERE name = 'IX_SalesOrderDetail_ColumnStore'
   GO

   SELECT * 
   FROM sys.dm_db_index_usage_stats
      WHERE database_id = DB_ID('AdventureWorks')
      AND object_id = OBJECT_ID('AdventureWorks.Sales.SalesOrderDetail');
   ```
   
## <a name="use-in-memory-oltp"></a>Usar o OLTP na memória
SQL Server fornece recursos de OLTP na memória que podem melhorar muito o desempenho dos sistemas de aplicativo.  Esta seção do guia de avaliação orientará você durante as etapas para criar uma tabela com otimização de memória armazenada na memória e um procedimento armazenado compilado nativamente que pode acessar a tabela sem a necessidade de ser compilado ou interpretado.

### <a name="configure-database-for-in-memory-oltp"></a>Configurar o banco de dados para OLTP na memória
1. É recomendável definir o banco de dados para um nível de compatibilidade de pelo menos 130 para usar o OLTP na memória.  Use a consulta a seguir para verificar o nível de compatibilidade atual do AdventureWorks:  

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

2. Quando uma transação envolve tanto uma tabela baseada em disco e uma tabela com otimização de memória, é essencial que a porção com otimização de memória da transação opere no nível de isolamento da transação chamado instantâneo.  Para impor com segurança este nível para tabelas com otimização de memória em uma transação entre contêineres, execute o seguinte:

   ```sql
   ALTER DATABASE CURRENT SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON
   GO
   ```

3. Antes de criar uma tabela com otimização de memória, você deve primeiro criar um grupo de arquivos de otimização de memória e um contêiner para arquivos de dados:

   ```sql
   ALTER DATABASE AdventureWorks ADD FILEGROUP AdventureWorks_mod CONTAINS memory_optimized_data
   GO  
   ALTER DATABASE AdventureWorks ADD FILE (NAME='AdventureWorks_mod', FILENAME='/var/opt/mssql/data/AdventureWorks_mod') TO FILEGROUP AdventureWorks_mod
   GO
   ```

### <a name="create-a-memory-optimized-table"></a>Criar uma tabela com otimização de memória
O armazenamento primário para tabelas com otimização de memória é memória principal e, portanto, ao contrário das tabelas baseadas em disco, dados não precisam ser lidos no disco em buffers de memória.  Para criar uma tabela com otimização de memória, use o MEMORY_OPTIMIZED = ON cláusula.

1. Execute a consulta a seguir para criar o tabela com otimização de memória dbo. ShoppingCart.  Por padrão, os dados serão mantidos no disco para fins de durabilidade (Observe que a durabilidade também pode ser definida para manter o esquema somente). 

   ```sql
   CREATE TABLE dbo.ShoppingCart ( 
   ShoppingCartId INT IDENTITY(1,1) PRIMARY KEY NONCLUSTERED,
   UserId INT NOT NULL INDEX ix_UserId NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000), 
   CreatedDate DATETIME2 NOT NULL, 
   TotalPrice MONEY
   ) WITH (MEMORY_OPTIMIZED=ON) 
   GO
   ```

2. Inseri alguns registros na tabela:

   ```sql
   INSERT dbo.ShoppingCart VALUES (8798, SYSDATETIME(), NULL) 
   INSERT dbo.ShoppingCart VALUES (23, SYSDATETIME(), 45.4) 
   INSERT dbo.ShoppingCart VALUES (80, SYSDATETIME(), NULL) 
   INSERT dbo.ShoppingCart VALUES (342, SYSDATETIME(), 65.4) 
   ```

### <a name="natively-compiled-stored-procedure"></a>Procedimento armazenado compilado nativamente
SQL Server dá suporte a procedimentos armazenados compilados nativamente que acessam tabelas com otimização de memória. As instruções T-SQL são compiladas para código de máquina e armazenadas como DLLs nativas, habilitando o acesso a dados mais rápido e execução de consulta mais eficiente que o T-SQL tradicional.   Os procedimentos armazenados que são marcados com NATIVE_COMPILATION são compilados nativamente. 

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
2. Inserir 1.000.000 linhas:

   ```sql
   EXEC usp_InsertSampleCarts 1000000 
   ```

3. Verifique se que as linhas foram inseridas:

   ```sql
   SELECT COUNT(*) FROM dbo.ShoppingCart 
   ```

### <a name="learn-more-about-in-memory-oltp"></a>Saiba mais sobre o OLTP na memória
Para obter mais informações sobre o OLTP na memória, consulte os tópicos a seguir:

- [Início Rápido 1: tecnologias do OLTP in-memory para um desempenho mais rápido do Transact-SQL](../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md)
- [Migrando para OLTP na memória](../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)
- [Tabela temporária e variável de tabela mais rápidas usando a otimização de memória](../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)
- [Monitorar e solucionar problemas de uso da memória](../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md)
- [OLTP na memória (otimização na memória)](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)

## <a name="use-query-store"></a>Use o repositório de consulta
Repositório de consultas coleta informações detalhadas sobre desempenho sobre consultas, planos de execução e estatísticas de tempo de execução.

Repositório de consultas não está ativo por padrão e pode ser habilitado com ALTER DATABASE:

   ```sql
   ALTER DATABASE AdventureWorks SET QUERY_STORE = ON;
   ```

Execute a seguinte consulta para retornar informações sobre consultas e planos no repositório de consultas: 

   ```sql
   SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*
   FROM sys.query_store_plan AS Pl
      JOIN sys.query_store_query AS Qry
         ON Pl.query_id = Qry.query_id
      JOIN sys.query_store_query_text AS Txt
         ON Qry.query_text_id = Txt.query_text_id ;
   ```

## <a name="query-dynamic-management-views"></a>Exibições de gerenciamento dinâmico de consulta
Exibições de gerenciamento dinâmico retornam informações de estado do servidor que podem ser usadas para monitorar a integridade de uma instância de servidor, diagnosticar problemas e ajustar o desempenho.

Para consultar a exibição de gerenciamento dinâmico dm_os_wait estatísticas:

   ```sql
   SELECT wait_type, wait_time_ms
   FROM sys.dm_os_wait_stats;
   ```

