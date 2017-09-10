---
title: DBCC CLEANTABLE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CLEANTABLE_TSQL
- DBCC_CLEANTABLE_TSQL
- DBCC CLEANTABLE
- CLEANTABLE
dev_langs:
- TSQL
helpviewer_keywords:
- disk space [SQL Server], reclaiming
- reclaiming space
- reallocating space
- removing columns
- DBCC CLEANTABLE statement
- space [SQL Server], reclaiming
- deleting columns
- dropping columns
ms.assetid: 0dbbc956-15b1-427b-812c-618a044d07fa
caps.latest.revision: 53
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7152b7241d97953fdeddf343dbeea60ed8d7ff5f
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-cleantable-transact-sql"></a>DBCC CLEANTABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]Recupera o espaço de colunas de comprimento variável descartadas em tabelas ou exibições indexadas.
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
  
DBCC CLEANTABLE  
(  
    { database_name | database_id | 0 }  
    , { table_name | table_id | view_name | view_id }  
    [ , batch_size ]  
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Database_Name* | *database_id* | 0  
 É o banco de dados ao qual pertence a tabela a ser limpa. Se 0 for especificado, será usado o banco de dados atual. Nomes de banco de dados devem seguir as regras para [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 *table_name* | *table_id* | *view_name*| *view_id*  
 É a tabela ou exibição indexada a ser limpa.  
  
 *batch_size*  
 É o número de linhas processadas por transação. Caso não especificado, ou se especificado 0, a instrução processará a tabela inteira em uma transação.  
  
 WITH NO_INFOMSGS  
 Suprime todas as mensagens informativas.  
  
## <a name="remarks"></a>Comentários  
DBCC CLEANTABLE recupera espaço depois que uma coluna de comprimento variável é descartada. Uma coluna de comprimento variável pode ser um dos seguintes tipos de dados: **varchar**, **nvarchar**, **varchar (max)**, **nvarchar (max)**, **varbinary**, **varbinary (max)**, **texto**, **ntext**, **imagem**,  **sql_variant**, e **xml**. O comando não recupera espaço depois que uma coluna de comprimento fixo é descartada.
Se as colunas descartadas forem armazenadas em linha, DBCC CLEANTABLE recuperará espaço da unidade de alocação IN_ROW_DATA da tabela. Se as colunas forem armazenadas fora de linha, o espaço será recuperado da unidade de alocação LOB_DATA ou ROW_OVERFLOW_DATA, dependendo do tipo de dados da coluna descartada. Se o espaço recuperado de uma página ROW_OVERFLOW_DATA ou LOB_DATA resultar em uma página vazia, DBCC CLEANTABLE removerá a página.
DBCC CLEANTABLE executa como uma ou mais transações. Se não for especificado um tamanho de lote, o comando processará a tabela inteira em uma transação e a tabela será bloqueada exclusivamente durante a operação. Para algumas tabelas grandes, o comprimento da única transação e o espaço do log requeridos podem ser muito grandes. Se um tamanho de lote for especificado, o comando executará em uma série de transações, cada qual incluindo o número especificado de linhas. DBCC CLEANTABLE não pode ser executado como uma transação dentro de outra transação.
Essa operação é totalmente registrada.
Não há suporte para DBCC CLEANTABLE para uso em tabelas do sistema, tabelas temporárias ou a parte do índice columnstore xVelocity de memória otimizada de uma tabela.
  
## <a name="best-practices"></a>Práticas recomendadas  
DBCC CLEANTABLE não deve ser executado como uma tarefa de manutenção de rotina. Em vez disso, use DBCC CLEANTABLE depois de fazer mudanças significativas em colunas de comprimento variável em uma tabela ou exibição indexada e precisar recuperar o espaço sem-uso prontamente. Como alternativa, é possível reconstruir os índices na tabela ou exibição; no entanto, essa é uma operação que utiliza muitos recursos.
  
## <a name="result-sets"></a>Conjuntos de resultados  
DBCC CLEANTABLE retorna:
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissões  
 Chamador deve possuir a tabela ou exibição indexada ou ser um membro do **sysadmin** função fixa de servidor a **db_owner** função de banco de dados fixa ou **db_ddladmin** função fixa de banco de dados.  
  
## <a name="examples"></a>Exemplos  
### <a name="a-using-dbcc-cleantable-to-reclaim-space"></a>A. Usando DBCC CLEANTABLE para recuperar espaço  
O exemplo a seguir executa DBCC CLEANTABLE para a tabela `Production.Document` no banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].
  
```sql  
DBCC CLEANTABLE (AdventureWorks2012,'Production.Document', 0)  
WITH NO_INFOMSGS;  
GO  
```  
  
### <a name="b-using-dbcc-cleantable-and-verifying-results"></a>B. Usando DBCC CLEANTABLE e verificando resultados  
O exemplo a seguir cria e popula uma tabela com várias colunas de comprimento variável. A seguir, duas das colunas são descartadas, e DBCC CLEANTABLE é executado para recuperar o espaço não utilizado. Uma consulta é executada para verificar os valores da contagem de página e espaço usado, antes e depois que o comando DBCC CLEANTABLE for executado.
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ('dbo.CleanTableTest', 'U') IS NOT NULL  
    DROP TABLE dbo.CleanTableTest;  
GO  
CREATE TABLE dbo.CleanTableTest  
    (FileName nvarchar(4000),   
    DocumentSummary nvarchar(max),  
    Document varbinary(max)  
    );  
GO  
-- Populate the table with data from the Production.Document table.  
INSERT INTO dbo.CleanTableTest  
    SELECT REPLICATE(FileName, 1000),   
           DocumentSummary,   
           Document  
    FROM Production.Document;  
GO  
-- Verify the current page counts and average space used in the dbo.CleanTableTest table.  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.CleanTableTest');  
SELECT alloc_unit_type_desc,   
       page_count,   
       avg_page_space_used_in_percent,   
       record_count  
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'Detailed');  
GO  
-- Drop two variable-length columns from the table.  
ALTER TABLE dbo.CleanTableTest  
DROP COLUMN FileName, Document;  
GO  
-- Verify the page counts and average space used in the dbo.CleanTableTest table  
-- Notice that the values have not changed.  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.CleanTableTest');  
SELECT alloc_unit_type_desc,   
       page_count,   
       avg_page_space_used_in_percent,   
       record_count  
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'Detailed');  
GO  
-- Run DBCC CLEANTABLE.  
DBCC CLEANTABLE (AdventureWorks2012,'dbo.CleanTableTest');  
GO  
-- Verify the values in the dbo.CleanTableTest table after the DBCC CLEANTABLE command.  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.CleanTableTest');  
SELECT alloc_unit_type_desc,   
       page_count,   
       avg_page_space_used_in_percent,   
       record_count  
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'Detailed');  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
 [sys. allocation_units &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)  
  
  

