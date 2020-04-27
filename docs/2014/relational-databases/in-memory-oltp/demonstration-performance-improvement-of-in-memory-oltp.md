---
title: 'Demonstração: melhoria do desempenho do OLTP in-memory | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c6def45d-d2d4-4d24-8068-fab4cd94d8cc
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 8c9477a318d2cb4f9886d67da8a4f8b5967cc180
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63071781"
---
# <a name="demonstration-performance-improvement-of-in-memory-oltp"></a>Demonstração: aprimoramento do desempenho do OLTP na memória
  Este exemplo mostra as melhorias de desempenho ao usar OLTP na Memória, comparando as diferenças nos tempos de resposta ao executar uma consulta Transact-SQL idêntica em tabelas baseadas em disco tradicionais e com otimização de memória. Além disso, um procedimento armazenado compilado nativamente também é criado (com base na mesma consulta) e executado para demonstrar que você normalmente obtém os melhores tempos de resposta ao consultar uma tabela com otimização de memória com um procedimento armazenado compilados nativamente. Este exemplo mostra apenas um aspecto das melhorias de desempenho ao acessar dados em tabelas com otimização de memória; a eficiência do acesso a dados ao executar inserções. Este exemplo é de thread único e não aproveita os benefícios de simultaneidade do OLTP na memória. Uma carga de trabalho que usa a simultaneidade apresentará um maior ganho de desempenho.  
  
> [!NOTE]  
>  Outro exemplo que demonstra as tabelas com otimização de memória está disponível em [Exemplos de OLTP na memória do SQL Server 2014](https://msftdbprodsamples.codeplex.com/releases/view/114491).  
  
 Para concluir este exemplo, você executará o seguinte:  
  
1.  Criar um banco de dados chamado **imoltp** e alterar seus detalhes do arquivo e configurá-lo para usar o OLTP na Memória.  
  
2.  Criar os objetos de banco de dados para o nosso exemplo: três tabelas e um procedimento armazenado compilado nativamente.  
  
3.  Executar as diferentes consultas e exibir os tempos de resposta para cada consulta.  
  
 Para configurar o banco de dados **imoltp** para nosso exemplo, crie primeiro uma pasta vazia: **c:\imoltp_data**, e, em seguida, execute o seguinte código:  
  
```sql  
USE master  
GO  
  
-- Create a new database.  
CREATE DATABASE imoltp  
GO  
  
-- Prepare the database for In-Memory OLTP by  
-- adding a memory-optimized filegroup to the database.  
ALTER DATABASE imoltp ADD FILEGROUP imoltp_file_group  
    CONTAINS MEMORY_OPTIMIZED_DATA;  
  
-- Add a file (to hold the memory-optimized data) to the new filegroup.  
ALTER DATABASE imoltp ADD FILE (name='imoltp_file', filename='c:\imoltp_data\imoltp_file')  
    TO FILEGROUP imoltp_file_group;  
GO  
  
```  
  
 Em seguida, execute o seguinte código para criar a tabela baseada em disco, 2 (duas) tabelas com otimização de memória e o procedimento armazenado compilado nativamente que será usado para demonstrar os métodos de acesso de dados diferentes:  
  
```sql  
USE imoltp  
GO  
  
-- If the tables or stored procedure already exist, drop them to start clean.  
IF EXISTS (SELECT NAME FROM sys.objects WHERE NAME = 'DiskBasedTable')  
   DROP TABLE [dbo].[DiskBasedTable]  
GO  
  
IF EXISTS (SELECT NAME FROM sys.objects WHERE NAME = 'InMemTable')  
   DROP TABLE [dbo].[InMemTable]  
GO  
  
IF EXISTS (SELECT NAME FROM sys.objects  WHERE NAME = 'InMemTable2')  
   DROP TABLE [dbo].[InMemTable2]  
GO  
  
IF EXISTS (SELECT NAME FROM sys.objects  WHERE NAME = 'usp_InsertData')  
   DROP PROCEDURE [dbo].[usp_InsertData]  
GO  
  
-- Create a traditional disk-based table.  
CREATE TABLE [dbo].[DiskBasedTable] (  
  c1 INT NOT NULL PRIMARY KEY,  
  c2 NCHAR(48) NOT NULL  
)  
GO  
  
-- Create a memory-optimized table.  
CREATE TABLE [dbo].[InMemTable] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
GO  
  
-- Create a 2nd memory-optimized table.  
CREATE TABLE [dbo].[InMemTable2] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
GO  
  
-- Create a natively-compiled stored procedure.  
CREATE PROCEDURE [dbo].[usp_InsertData]   
  @rowcount INT,  
  @c NCHAR(48)  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
  AS   
  BEGIN ATOMIC   
  WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  DECLARE @i INT = 1;  
  WHILE @i <= @rowcount  
  BEGIN  
    INSERT INTO [dbo].[inMemTable2](c1,c2) VALUES (@i, @c);  
    SET @i += 1;  
  END  
END  
GO  
  
```  
  
 A instalação foi concluída e você está pronto para executar as consultas que exibirão os tempos de resposta comparando o desempenho entre os métodos de acesso de dados.  
  
 Para concluir o exemplo, execute o seguinte código várias vezes. Ignore os resultados da primeira execução, que são afetados negativamente pela alocação de memória inicial.  
  
```sql  
SET STATISTICS TIME OFF;  
SET NOCOUNT ON;  
  
-- Delete data from all tables to reset the example.  
DELETE FROM [dbo].[DiskBasedTable]   
    WHERE [c1]>0  
GO  
DELETE FROM [dbo].[inMemTable]   
    WHERE [c1]>0  
GO  
DELETE FROM [dbo].[InMemTable2]   
    WHERE [c1]>0  
GO  
  
-- Declare parameters for the test queries.  
DECLARE @i INT = 1;  
DECLARE @rowcount INT = 100000;  
DECLARE @c NCHAR(48) = N'12345678901234567890123456789012345678';  
DECLARE @timems INT;  
DECLARE @starttime datetime2 = sysdatetime();  
  
-- Disk-based table queried with interpreted Transact-SQL.  
BEGIN TRAN  
  WHILE @I <= @rowcount  
  BEGIN  
    INSERT INTO [dbo].[DiskBasedTable](c1,c2) VALUES (@i, @c);  
    SET @i += 1;  
  END  
COMMIT  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT CAST(@timems AS VARCHAR(10)) + ' ms (disk-based table with interpreted Transact-SQL).';  
  
-- Memory-optimized table queried with interpreted Transact-SQL.  
SET @i = 1;  
SET @starttime = sysdatetime();  
  
BEGIN TRAN  
  WHILE @i <= @rowcount  
    BEGIN  
      INSERT INTO [dbo].[InMemTable](c1,c2) VALUES (@i, @c);  
      SET @i += 1;  
    END  
COMMIT  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT CAST(@timems AS VARCHAR(10)) + ' ms (memory-optimized table with interpreted Transact-SQL).';  
  
-- Memory-optimized table queried with a natively-compiled stored procedure.  
SET @starttime = sysdatetime();  
  
EXEC usp_InsertData @rowcount, @c;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT CAST(@timems AS VARCHAR(10)) + ' ms (memory-optimized table with natively-compiled stored procedure).';  
  
```  
  
 Os resultados esperados fornecem tempos de resposta reais mostrando como usar tabelas com otimização de e procedimentos armazenados compilados nativamente normalmente fornecem tempos de resposta consistentemente mais rápidos que as mesmas cargas de trabalho executadas em tabelas baseadas em disco tradicionais.  
  
## <a name="see-also"></a>Consulte Também  
 [Extensões para o AdventureWorks para demonstrar o OLTP na memória](../../database-engine/extensions-to-adventureworks-to-demonstrate-in-memory-oltp.md)   
 [O OLTP na memória &#40;a otimização na memória&#41;](in-memory-oltp-in-memory-optimization.md)   
 [Tabelas com otimização de memória](memory-optimized-tables.md)   
 [Procedimentos armazenados compilados nativamente](natively-compiled-stored-procedures.md)   
 [Requisitos para usar tabelas com otimização de memória](requirements-for-using-memory-optimized-tables.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [Opções de arquivo e grupo de arquivos ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)   
 [CRIAR procedimento e tabelas com otimização de memória](/sql/t-sql/statements/create-procedure-transact-sql)  
  
  
