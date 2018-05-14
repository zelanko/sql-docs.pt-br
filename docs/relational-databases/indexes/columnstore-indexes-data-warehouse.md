---
title: Índices columnstore – Data Warehouse | Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 21fd153b-116d-47fc-a926-f1528299a391
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4d9d0cffae7388f21b6df32e51669b946099a1c2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="columnstore-indexes---data-warehouse"></a>Índices columnstore – Data Warehouse
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Os índices columnstore, junto com o particionamento, são essenciais para criar um data warehouse do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="whats-new"></a>Novidades  
 O[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] introduz estes recursos para melhorias de desempenho de columnstore:  
  
-   O AlwaysOn dá suporte à consulta de um índice columnstore em uma réplica secundária legível.  
-   O MARS (Multiple Active Result Sets) oferece suporte aos índices columnstore.  
-   Uma nova exibição de gerenciamento dinâmico [sys.dm_db_column_store_row_group_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md) fornece informações em nível de grupo de linhas de solução de problemas de desempenho.  
-   Consultas de thread único nos índices columnstore podem ser executadas em modo de lote. Anteriormente, somente consultas multithread podiam ser executadas em modo de lote.  
-   O operador `SORT` é executado no modo de lote.  
-   Várias operações `DISTINCT` são executadas no modo de lote.  
-   As Agregações de Janela agora são executadas no modo de lote no nível de compatibilidade do banco de dados 130 e superior.  
-   Aplicação de agregação para processamento eficiente de agregações. Isso tem suporte em todos os níveis de compatibilidade de banco de dados.  
-   Aplicação de predicado de cadeia de caracteres para o processamento eficiente dos predicados de cadeia de caracteres. Isso tem suporte em todos os níveis de compatibilidade de banco de dados.  
-   Isolamento de instantâneo no nível de compatibilidade do banco de dados 130 e superior.  
  
## <a name="improve-performance-by-combining-nonclustered-and-columnstore-indexes"></a>Melhora o desempenho combinando índices não clusterizado e columnstore  
 Do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]em diante, é possível definir índices não clusterizados em um índice columnstore clusterizado.   
  
### <a name="example-improve-efficiency-of-table-seeks-with-a-nonclustered-index"></a>Exemplo: melhorar a eficiência de buscas de tabelas com um índice não clusterizado  
 Para melhorar a eficiência das buscas de tabelas em um data warehouse, você pode criar um índice não clusterizado projetado para executar consultas que executam melhor com as buscas de tabelas. Por exemplo, as consultas que procuram valores correspondentes ou retornam um pequeno intervalo de valores terão um desempenho melhor em um índice de árvore B em vez de um índice columnstore. Elas não exigem uma verificação de tabela completa por meio do índice columnstore e retornarão o resultado correto com mais rapidez, fazendo uma pesquisa binária por meio de um índice de árvore B.  
  
```sql  
--BASIC EXAMPLE: Create a nonclustered index on a columnstore table.  
  
--Create the table  
CREATE TABLE t_account (  
    AccountKey int NOT NULL,  
    AccountDescription nvarchar (50),  
    AccountType nvarchar(50),  
    UnitSold int  
);  
GO  
  
--Store the table as a columnstore.  
CREATE CLUSTERED COLUMNSTORE INDEX taccount_cci ON t_account;  
GO  
  
--Add a nonclustered index.  
CREATE UNIQUE INDEX taccount_nc1 ON t_account (AccountKey);  
```  
  
### <a name="example-use-a-nonclustered-index-to-enforce-a-primary-key-constraint-on-a-columnstore-table"></a>Exemplo: use um índice não clusterizado para impor uma restrição de chave primária em um tabela columnstore.  
 Por padrão, uma tabela columnstore não permite uma restrição de chave primária. Agora você pode usar um índice não clusterizado em uma tabela columnstore para impor uma restrição de chave primária. Uma chave primária é equivalente a uma restrição UNIQUE em uma coluna não NULL e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] implementa uma restrição UNIQUE como um índice não clusterizado. Combinando esses fatos, o exemplo a seguir define uma restrição UNIQUE na accountkey da coluna não NULL. O resultado é um índice não clusterizado que impõe uma restrição de chave primária como uma restrição UNIQUE em uma coluna não NULL.  
  
 Em seguida, a tabela é convertida em um índice columnstore clusterizado. Durante a conversão, o índice não clusterizado persiste. O resultado é um índice columnstore clusterizado com um índice não clusterizado que impõe a restrição de chave primária. Uma vez que qualquer atualização ou inserção na tabela columnstore também afetará o índice não clusterizado, todas as operações que violarem a restrição exclusiva e o não NULL causarão a falha de toda a operação.  
  
 O resultado é um índice columnstore com um índice não clusterizado que impõe uma restrição de chave primária nos dois índices.  
  
```sql 
--EXAMPLE: Enforce a primary key constraint on a columnstore table.   
  
--Create a rowstore table with a unique constraint.  
--The unique constraint is implemented as a nonclustered index.  
CREATE TABLE t_account (  
    AccountKey int NOT NULL,  
    AccountDescription nvarchar (50),  
    AccountType nvarchar(50),  
    UnitSold int,  
  
    CONSTRAINT uniq_account UNIQUE (AccountKey)  
);  
  
--Store the table as a columnstore.   
--The unique constraint is preserved as a nonclustered index on the columnstore table.  
CREATE CLUSTERED COLUMNSTORE INDEX t_account_cci ON t_account  
  
--By using the previous two steps, every row in the table meets the UNIQUE constraint  
--on a non-NULL column.  
--This has the same end-result as having a primary key constraint  
--All updates and inserts must meet the unique constraint on the nonclustered index or they will fail.  
  
--If desired, add a foreign key constraint on AccountKey.  
  
ALTER TABLE [dbo].[t_account]  
WITH CHECK ADD FOREIGN KEY([AccountKey]) REFERENCES my_dimension(Accountkey); 
```  
  
### <a name="improve-performance-by-enabling-row-level-and-row-group-level-locking"></a>Melhorar o desempenho permitindo o bloqueio no nível da linha e no nível do grupo de linhas  
 Para complementar o índice não clusterizado em um recurso de índice columnstore, o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] oferece o recurso de bloqueio granular para selecionar, atualizar e excluir operações. É possível executar consultas com o bloqueio no nível de linha em buscas de índice com base em um índice não clusterizado, e um bloqueio no nível do grupo de linhas em verificações de tabela completa com base no índice columnstore. Use isto para alcançar maior simultaneidade de leitura/gravação usando adequadamente o bloqueio no nível de linha e no nível do grupo de linhas.  
  
```sql  
--Granular locking example  
--Store table t_account as a columnstore table.  
CREATE CLUSTERED COLUMNSTORE INDEX taccount_cci ON t_account  
GO  
  
--Add a nonclustered index for use with this example  
CREATE UNIQUE INDEX taccount_nc1 ON t_account (AccountKey);  
GO  
  
--Look at locking with access through the nonclustered index  
SET TRANSACTION ISOLATION LEVEL repeatable read;  
GO  
  
BEGIN TRAN  
    -- The query plan chooses a seek operation on the nonclustered index  
    -- and takes the row lock  
    SELECT * FROM t_account WHERE AccountKey = 100;  
END TRAN  
```  
  
### <a name="snapshot-isolation-and-read-committed-snapshot-isolations"></a>Isolamento de instantâneo e isolamentos de instantâneo de leitura confirmada  
 Use o SI (isolamento de instantâneo) para garantir a consistência transacional, e os RCSI (isolamentos de instantâneo de leitura confirmada) para garantir a consistência no nível da instrução para consultas em índices columnstore. Isso permite que as consultas sejam executadas sem bloquear os gravadores de dados. Esse comportamento de não bloqueio também reduz consideravelmente a probabilidade de deadlocks para transações complexas. Para saber mais, confira [Isolamento de instantâneo no SQL Server](http://msdn.microsoft.com/library/tcbchxcb\(v=vs.110\).aspx) no MSDN.  
  
## <a name="see-also"></a>Consulte Também  
 [Diretrizes de design dos Índices columnstore](../../relational-databases/indexes/columnstore-indexes-design-guidance.md)   
 [Diretrizes de Carregamento de Dados de Índices columnstore](../../relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)   
 [Desempenho de consultas de Índices columnstore](../../relational-databases/indexes/columnstore-indexes-query-performance.md)   
 [Introdução ao Columnstore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
 [Desfragmentação de índices columnstore](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)  
 [Arquitetura de índices columnstore](../../relational-databases/sql-server-index-design-guide.md#columnstore_index) 
  
