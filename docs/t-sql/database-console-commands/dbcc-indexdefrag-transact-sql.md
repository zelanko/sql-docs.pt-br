---
title: DBCC INDEXDEFRAG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|database-console-commands
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- INDEXDEFRAG
- DBCC INDEXDEFRAG
- DBCC_INDEXDEFRAG_TSQL
- INDEXDEFRAG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- defragmenting indexes
- DBCC INDEXDEFRAG statement
- leaf level defragmenting
- fragmentation [SQL Server]
- index defragmenting [SQL Server]
ms.assetid: 3c7df676-4843-44d0-8c1c-a9ab7e593b70
caps.latest.revision: 49
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 474be1cd3f0d81e6247cbbf69544ab8ca436274e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="dbcc-indexdefrag-transact-sql"></a>DBCC INDEXDEFRAG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Desfragmenta índices da tabela ou exibição especificada.
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) nesse caso.  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658))
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DBCC INDEXDEFRAG  
(  
    { database_name | database_id | 0 }   
    , { table_name | table_id | view_name | view_id }   
    [ , { index_name | index_id } [ , { partition_number | 0 } ] ]  
)  
    [ WITH NO_INFOMSGS ]   
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name* | *database_id* | 0  
 É o banco de dados que contém o índice a desfragmentar. Se 0 for especificado, será usado o banco de dados atual. Os nomes de banco de dados precisam estar em conformidade com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 *table_name* | *table_id* | *view_name* | *view_id*  
 É a tabela ou exibição que contém o índice a desfragmentar. Os nomes de tabelas e exibições devem obedecer às regras de identificadores.  
  
 *index_name* | *index_id*  
 É o ID ou o nome do índice a ser desfragmentado. Se não for especificado, a instrução desfragmentará todos os índices da tabela ou exibição especificada. Os nomes de índice devem obedecer às regras para identificadores.  
  
 *partition_number* | 0  
 É o número de partição do índice a desfragmentar. Se não for especificado ou se for especificado 0, a instrução desfragmentará todas as partições no índice especificado.  
  
 WITH NO_INFOMSGS  
 Suprime todas as mensagens informativas com níveis de severidade de 0 a 10.  
  
## <a name="remarks"></a>Remarks  
DBCC INDEXDEFRAG desfragmenta o nível folha de um índice de forma que a ordem física das páginas corresponda à ordem lógica da esquerda para a direita dos nós folha, melhorando assim o desempenho do exame do índice.
  
> [!NOTE]  
>  Quando DBCC INDEXDEFRAG é executado, a desfragmentação de índice ocorre em série. Isso significa que a operação em um único índice que usa um único thread é executada. Nenhum paralelismo ocorre. Além disso, operações em vários índices da mesma instrução DBCC INDEXDEFRAG são executadas em um índice por vez.  
  
DBCC INDEXDEFRAG também compacta as páginas de um índice, levando em consideração o fator de preenchimento especificado quando o índice foi criado. Qualquer página vazia criada por causa desta compactação é removida. Para obter mais informações, veja [Especificar fator de preenchimento para um índice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md).
  
Se um índice se estender por mais de um arquivo, DBCC INDEXDEFRAG desfragmentará um arquivo por vez. As páginas não migram entre arquivos.
  
DBCC INDEXDEFRAG informa a porcentagem estimada de conclusão a cada cinco minutos. DBCC INDEXDEFRAG pode ser finalizada a qualquer momento do processo e qualquer trabalho concluído é retido.
  
Ao contrário de DBCC DBREINDEX ou da operação de criação de índices em geral, DBCC INDEXDEFRAG é uma operação online. Não mantém bloqueios por longos períodos. Por isso, DBCC INDEXDEFRAG não bloqueia a execução de consultas ou atualizações. Como o tempo de desfragmentação está relacionado ao nível de fragmentação, um índice relativamente não fragmentado pode ser desfragmentado mais rápido do que a criação de um novo índice. Um índice muito fragmentado pode levar muito mais tempo para ser desfragmentado do que para ser recriado.
  
A desfragmentação é sempre totalmente armazenada em log, independentemente da configuração do modelo de recuperação do banco de dados. Para obter mais informações, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md). A desfragmentação de um índice muito fragmentado pode gerar mais logs do que uma criação de índice totalmente registrada em log. Entretanto, a desfragmentação é executada como uma série de transações curtas; dessa forma, um log maior será desnecessário se os backups de log forem feitos com frequência ou se a configuração do modelo de recuperação for SIMPLE.
  
## <a name="restrictions"></a>Restrictions  
DBCC INDEXDEFRAG mistura as páginas de folha de índice no lugar. Por isso, se um índice for intercalado com outros índices no disco, a execução de DBCC INDEXDEFRAG para esse índice não deixará todas as páginas de folha do índice contíguas. Para melhorar a clusterização de páginas, recrie o índice.
DBCC INDEXDEFRAG não pode ser usado para desfragmentar os seguintes índices:
-   Um índice desabilitado.  
-   Um índice com bloqueio de página definido como OFF.  
-   Um índice espacial.  
  
Não há suporte nas tabelas do sistema para o uso de DBCC INDEXDEFRAG.
  
## <a name="result-sets"></a>Conjuntos de resultados  
DBCC INDEXDEFRAG retornará o seguinte conjunto de resultados (os valores podem variar) se um índice for especificado na instrução (a menos que WITH NO_INFOMSGS seja especificado):
  
```sql
Pages Scanned Pages Moved Pages Removed  
------------- ----------- -------------  
359           346         8  
  
(1 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissões  
O chamador precisa ser o proprietário da tabela ou ser membro da função de servidor fixa **sysadmin**, da função de banco de dados fixa **db_owner** ou da função de banco de dados fixa **db_ddladmin**.
  
## <a name="examples"></a>Exemplos  
### <a name="a-using-dbcc-indexdefrag-to-defragment-an-index"></a>A. Usando DBCC INDEXDEFRAG para desfragmentar um índice  
O exemplo a seguir desfragmenta todas as partições do índice `PK_Product_ProductID` na tabela `Production.Product` no banco de dados `AdventureWorks`.
  
```sql  
DBCC INDEXDEFRAG (AdventureWorks2012, 'Production.Product', PK_Product_ProductID);  
GO  
```  
  
### <a name="b-using-dbcc-showcontig-and-dbcc-indexdefrag-to-defragment-the-indexes-in-a-database"></a>B. Usando DBCC SHOWCONTIG e DBCC INDEXDEFRAG para desfragmentar os índices em um banco de dados  
 O exemplo a seguir mostra uma forma simples de desfragmentar todos os índices de um banco de dados que estão fragmentados acima de um limite declarado.  
  
```sql  
/*Perform a 'USE <database name>' to select the database in which to run the script.*/  
-- Declare variables  
SET NOCOUNT ON;  
DECLARE @tablename varchar(255);  
DECLARE @execstr   varchar(400);  
DECLARE @objectid  int;  
DECLARE @indexid   int;  
DECLARE @frag      decimal;  
DECLARE @maxfrag   decimal;  
  
-- Decide on the maximum fragmentation to allow for.  
SELECT @maxfrag = 30.0;  
  
-- Declare a cursor.  
DECLARE tables CURSOR FOR  
   SELECT TABLE_SCHEMA + '.' + TABLE_NAME  
   FROM INFORMATION_SCHEMA.TABLES  
   WHERE TABLE_TYPE = 'BASE TABLE';  
  
-- Create the table.  
CREATE TABLE #fraglist (  
   ObjectName char(255),  
   ObjectId int,  
   IndexName char(255),  
   IndexId int,  
   Lvl int,  
   CountPages int,  
   CountRows int,  
   MinRecSize int,  
   MaxRecSize int,  
   AvgRecSize int,  
   ForRecCount int,  
   Extents int,  
   ExtentSwitches int,  
   AvgFreeBytes int,  
   AvgPageDensity int,  
   ScanDensity decimal,  
   BestCount int,  
   ActualCount int,  
   LogicalFrag decimal,  
   ExtentFrag decimal);  
  
-- Open the cursor.  
OPEN tables;  
  
-- Loop through all the tables in the database.  
FETCH NEXT  
   FROM tables  
   INTO @tablename;  
  
WHILE @@FETCH_STATUS = 0  
BEGIN  
-- Do the showcontig of all indexes of the table  
   INSERT INTO #fraglist   
   EXEC ('DBCC SHOWCONTIG (''' + @tablename + ''')   
      WITH FAST, TABLERESULTS, ALL_INDEXES, NO_INFOMSGS');  
   FETCH NEXT  
      FROM tables  
      INTO @tablename;  
END;  
  
-- Close and deallocate the cursor.  
CLOSE tables;  
DEALLOCATE tables;  
  
-- Declare the cursor for the list of indexes to be defragged.  
DECLARE indexes CURSOR FOR  
   SELECT ObjectName, ObjectId, IndexId, LogicalFrag  
   FROM #fraglist  
   WHERE LogicalFrag >= @maxfrag  
      AND INDEXPROPERTY (ObjectId, IndexName, 'IndexDepth') > 0;  
  
-- Open the cursor.  
OPEN indexes;  
  
-- Loop through the indexes.  
FETCH NEXT  
   FROM indexes  
   INTO @tablename, @objectid, @indexid, @frag;  
  
WHILE @@FETCH_STATUS = 0  
BEGIN  
   PRINT 'Executing DBCC INDEXDEFRAG (0, ' + RTRIM(@tablename) + ',  
      ' + RTRIM(@indexid) + ') - fragmentation currently '  
       + RTRIM(CONVERT(varchar(15),@frag)) + '%';  
   SELECT @execstr = 'DBCC INDEXDEFRAG (0, ' + RTRIM(@objectid) + ',  
       ' + RTRIM(@indexid) + ')';  
   EXEC (@execstr);  
  
   FETCH NEXT  
      FROM indexes  
      INTO @tablename, @objectid, @indexid, @frag;  
END;  
  
-- Close and deallocate the cursor.  
CLOSE indexes;  
DEALLOCATE indexes;  
  
-- Delete the temporary table.  
DROP TABLE #fraglist;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)
  
  

