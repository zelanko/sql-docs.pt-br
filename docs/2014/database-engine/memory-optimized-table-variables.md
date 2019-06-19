---
title: Variáveis de tabela com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: bd102e95-53e2-4da6-9b8b-0e4f02d286d3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 485f481819a9712f822f969c04d8e7050ad43bae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62774401"
---
# <a name="memory-optimized-table-variables"></a>Variáveis de tabela com otimização de memória
  Além das tabelas com otimização de memória (para acesso eficiente a dados) e dos procedimentos armazenados compilados nativamente (para processamento eficiente de consulta e execução de lógica de negócios), o [!INCLUDE[hek_2](../includes/hek-2-md.md)] apresenta um terceiro tipo de objeto: o tipo de tabela com otimização de memória. Uma variável de tabela criada usando um tipo de tabela com otimização de memória é uma variável de tabela com otimização de memória.  
  
 As variáveis de tabela com otimização de memória oferecem as seguintes vantagens em comparação com as variáveis de tabela baseada em disco:  
  
-   As variáveis são armazenadas apenas na memória. O acesso a dados é mais eficiente, pois o tipo de tabela com otimização de memória usa o mesmo algoritmo com otimização de memória e estrutura de dados utilizados para tabelas com otimização de memória, especialmente quando as variáveis são usadas em procedimentos armazenados compilados nativamente.  
  
-   Com as variáveis de tabela com otimização de memória, não há utilização de tempdb. As variáveis de tabela não são armazenados em tempdb e não usam nenhum recurso em tempdb.  
  
 Os cenários de uso típicos para variáveis de tabela com otimização de memória são:  
  
-   Armazenar resultados intermediários e criar conjuntos de resultados únicos com base em várias consultas nos procedimentos armazenados compilados nativamente.  
  
-   Passar parâmetros com valor de tabela para procedimentos armazenados compilados nativamente e procedimentos armazenados interpretados.  
  
-   Substituir variáveis de tabela baseadas em disco e, em alguns casos, tabelas #temp que são locais para um procedimento armazenado. Isso será particularmente útil se houver muita contenção de tempdb no sistema.  
  
-   As variáveis de tabela podem ser usados para simular cursores em procedimentos armazenados compilados nativamente, de modo que possam ajudar você a contornar as restrições da área da superfície em procedimentos armazenados compilados nativamente.  
  
 Como as tabelas com otimização de memória, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] gera uma DLL para cada tipo de tabela com otimização de memória. (Compilação é invocada quando o tipo de tabela com otimização de memória é criado e não quando usado para criar variáveis de tabela com otimização de memória). Essa DLL inclui as funções para acessar índices e recuperar dados de variáveis de tabela. Quando uma variável de tabela com otimização de memória é declarada com base no tipo de tabela, uma instância da tabela e das estruturas de índice correspondentes ao tipo de tabela é criada na sessão do usuário. A variável de tabela pode ser usada da mesma maneira que as variáveis de tabela baseadas em disco. Você pode inserir, atualizar e excluir linhas na variável de tabela e usar variáveis em consultas do [!INCLUDE[tsql](../includes/tsql-md.md)] . Você também pode passar as variáveis para procedimentos armazenados compilados nativamente e interpretados, como parâmetros com valor de tabela (TVP).  
  
 O exemplo a seguir mostra um tipo de tabela com otimização de memória do exemplo o OLTP na memória com base no AdventureWorks ([exemplo de OLTP na memória do SQL Server 2014](https://msftdbprodsamples.codeplex.com/releases/view/114491)).  
  
```sql
CREATE TYPE Sales.SalesOrderDetailType_inmem
   AS TABLE
(
   OrderQty         smallint   NOT NULL,
   ProductID        int        NOT NULL,

   SpecialOfferID   int        NOT NULL
      INDEX  IX_SpecialOfferID  NONCLUSTERED,

   LocalID          int        NOT NULL,

   INDEX IX_ProductID HASH (ProductID)
      WITH ( BUCKET_COUNT = 8 )
)
WITH ( MEMORY_OPTIMIZED = ON );
```  
  
 O exemplo a seguir mostra que a sintaxe de tipos de tabela com otimização de memória é semelhante aos tipos de tabela baseados em disco, com as seguintes exceções:  
  
-   `MEMORY_OPTIMIZED=ON` indica se o tipo de tabela tem otimização de memória.  
  
-   O tipo deve ter pelo menos um índice. Assim como ocorre com as tabelas com otimização de memória, você pode usar índices de hash e não clusterizados.  
  
     Para um índice de hash, o número de buckets deve ser de cerca de uma a duas vezes o número de chaves de índice exclusivo esperado. Para obter mais informações, consulte [Determining the Correct Bucket Count for Hash Indexes](../relational-databases/indexes/indexes.md).  
  
-   O tipo de dados e as restrições da restrição nas tabelas com otimização de memória também se aplicam aos tipos de tabela com otimização de memória. Por exemplo, no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] há suporte para as restrições padrão, mas as restrições de verificação não têm esse suporte.  
  
 Assim como ocorre com as tabelas com otimização de memória, as variáveis de tabela com otimização de memória,  
  
-   Não oferecem suporte a planos paralelos.  
  
-   Deve ajustar à memória e não usar recursos de disco.  
  
 As variáveis de tabela baseada em disco existem em tempdb. As variáveis de tabela com otimização de memória existem no banco de dados do usuário (mas não consomem armazenamento e não são recuperadas).  
  
 Você não pode criar uma variável de tabela com otimização de memória usando sintaxe de linha. Diferentemente das variáveis de tabela baseadas em disco, você deve criar um tipo primeiro.  
  
## <a name="table-valued-parameters"></a>Parâmetros com valor de tabela  
 O exemplo de script a seguir mostra a declaração de uma variável de tabela como o tipo de tabela com otimização de memória `Sales.SalesOrderDetailType_inmem`, a inserção de três linhas na variável e a passagem da variável como um TVP para `Sales.usp_InsertSalesOrder_inmem`.  
  
```sql  
DECLARE @od Sales.SalesOrderDetailType_inmem,  
  @SalesOrderID uniqueidentifier,  
  @DueDate datetime2 = SYSDATETIME()  
  
INSERT @od (LocalID, ProductID, OrderQty, SpecialOfferID) VALUES  
  (1, 888, 2, 1),  
  (2, 450, 13, 1),  
  (3, 841, 1, 1)  
  
EXEC Sales.usp_InsertSalesOrder_inmem  
  @SalesOrderID = @SalesOrderID,  
  @DueDate = @DueDate,  
 @OnlineOrderFlag = 1,  
  @SalesOrderDetails = @od  
```  
  
 Os tipos de tabela com otimização de memória podem ser usados como o tipo para parâmetros com valor de tabela (TVPs) de procedimento armazenado e podem ser referenciados pelos clientes exatamente da mesma forma que os tipos de tabelas baseadas em disco e TVPs. Assim, a chamada de procedimentos armazenados com TVPs com otimização de memória e procedimentos armazenados compilados nativamente funciona exatamente da mesma forma que a chamada de procedimentos armazenados interpretados com TVPs baseadas em disco.  
  
## <a name="temp-table-replacement"></a>#temp Substituição de tabela  
 O exemplo a seguir mostra tipos de tabela com otimização de memória e variáveis de tabela em substituição a tabelas #temp locais para um procedimento armazenado.  
  
```sql  
-- Using SQL procedure and temp table  
CREATE TABLE #tempTable (c INT NOT NULL PRIMARY KEY NONCLUSTERED)  
  
CREATE PROCEDURE sqlProc  
AS  
BEGIN  
  TRUNCATE TABLE #tempTable  
  
  INSERT #tempTable VALUES (1)  
  INSERT #tempTable VALUES (2)  
  INSERT #tempTable VALUES (3)  
  SELECT * FROM #tempTable  
END  
GO  
  
-- Using natively compiled stored procedure and table variable  
CREATE TYPE TT AS TABLE (c INT NOT NULL PRIMARY KEY NONCLUSTERED)  
GO  
  
CREATE PROCEDURE NCSPProc  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  DECLARE @tableVariable TT  
  INSERT @tableVariable VALUES (1)  
  INSERT @tableVariable VALUES (2)  
  INSERT @tableVariable VALUES (3)  
  SELECT c FROM @tableVariable  
END  
GO  
```  
  
## <a name="creating-a-single-result-set"></a>Criando um único conjunto de resultados  
 O exemplo a seguir mostra como armazenar os resultados intermediários e criar conjuntos de resultados únicos com base em várias consultas em procedimentos armazenados compilados nativamente. O exemplo está calculando a união `SELECT c1 FROM dbo.t1 UNION SELECT c1 FROM dbo.t2`.  
  
```sql  
CREATE DATABASE hk  
GO  
ALTER DATABASE hk ADD FILEGROUP hk_mod CONTAINS MEMORY_OPTIMIZED_DATA  
ALTER DATABASE hk ADD FILE( NAME = 'hk_mod' , FILENAME = 'c:\data\hk_mod') TO FILEGROUP hk_mod;  
  
USE hk  
GO  
  
CREATE TYPE tab1 AS TABLE (c1 INT NOT NULL, INDEX idx NONCLUSTERED(c1)) WITH (MEMORY_OPTIMIZED = ON)  
  
CREATE TABLE dbo.t1 (c1 INT NOT NULL, INDEX idx NONCLUSTERED(c1)) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
CREATE TABLE dbo.t2 (c1 INT NOT NULL, INDEX idx NONCLUSTERED(c1)) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
  
INSERT INTO dbo.t1 VALUES (1), (2)  
INSERT INTO dbo.t2 VALUES (3), (4)  
GO  
  
CREATE PROCEDURE dbo.p1  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
  AS  
  BEGIN ATOMIC WITH ( TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english' )  
  
    DECLARE @t dbo.tab1  
    INSERT @t (c1)  
    SELECT c1 FROM dbo.t1;  
  
    INSERT @t (c1)  
    SELECT c1 FROM dbo.t2;  
  
    SELECT c1 FROM @t;  
  END  
GO  
  
EXEC dbo.p1  
GO  
```  
  
## <a name="memory-consumption-for-table-variables"></a>Consumo de memória para variáveis de tabela  
 O consumo de memória para variáveis de tabela é semelhante às tabelas com otimização de memória, com a exceção dos índices não clusterizados. Se você inserir várias linhas em variáveis de tabela com otimização de memória com índices não clusterizados e se as chaves do índice forem grandes, essas variáveis de tabela usarão uma quantidade desproporcional de memória. Os índices não clusterizados em variáveis de grandes tabelas exige que proporcionalmente mais memória que um índice não clusterizado exigiria para o mesmo número de linhas inseridas em uma tabela (mais memória nas páginas de índice).  
  
 A memória para variáveis de tabela é obtida do pool de recursos do administrador de recursos do banco de dados.  
  
 Ao contrário das tabelas com otimização de memória, a memória consumida (incluindo linhas excluídas) por variáveis de tabela é liberada quando a variável de tabela sai do escopo.  
  
 A memória é contabilizada como parte de um único consumidor de memória de PGPOOL do banco de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Suporte ao Transact-SQL para OLTP in-memory](../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)  
  
  
