---
title: DROP TABLE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_TABLE_TSQL
- DROP TABLE
dev_langs: TSQL
helpviewer_keywords:
- removing indexes
- table removal [SQL Server]
- deleting indexes
- dropping data
- deleting tables
- dropping indexes
- removing constraints
- removing permissions
- DROP TABLE statement
- removing tables
- deleting triggers
- removing data
- dropping tables
- deleting permissions
- dropping triggers
- deleting constraints
- removing triggers
- deleting data
- dropping constraints
- dropping permissions
ms.assetid: 0b6f2b6f-3aa3-4767-943f-43df3c3c5cfd
caps.latest.revision: "61"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: df9843e4b72c6a8092756725d1d4b3f96eefec74
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="drop-table-transact-sql"></a>DROP TABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Remove uma ou mais definições de tabela e todos os dados, índices, gatilhos, restrições e especificações de permissão dessas tabelas. Qualquer exibição ou procedimento armazenado que faz referência à tabela descartada deverá ser explicitamente removido usando [DROP VIEW](../../t-sql/statements/drop-view-transact-sql.md) ou [DROP PROCEDURE](../../t-sql/statements/drop-procedure-transact-sql.md). Para relatar as dependências em uma tabela, use [sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP TABLE [ IF EXISTS ] [ database_name . [ schema_name ] . | schema_name . ]  
table_name [ ,...n ]  
[ ; ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name   
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 É o nome do banco de dados no qual a tabela foi criada.  
  
 O Banco de Dados SQL do Windows Azure oferece suporte ao formato de nome de três partes database_name.[schema_name].object_name quando o database_name é o banco de dados atual ou o database_name é tempdb e o object_name começa com #. O Banco de Dados SQL do Windows Azure não oferece suporte a nomes de quatro partes.  
  
 *SE EXISTIR*  
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Condicionalmente descarta a tabela somente se ele já existe.  
  
 *schema_name*  
 É o nome do esquema ao qual a tabela pertence.  
  
 *table_name*  
 É o nome da tabela a ser removida.  
  
## <a name="remarks"></a>Comentários  
 DROP TABLE não pode ser usado para descartar uma tabela que é referenciada por uma restrição FOREIGN KEY. A restrição FOREIGN KEY que faz referência ou a tabela de referência deve ser primeiramente descartada. Se a tabela de referência e a tabela que contém a chave primária forem descartadas na mesma instrução DROP TABLE, a tabela de referência deverá ser listada em primeiro lugar.  
  
 Podem ser descartadas várias tabelas em qualquer banco de dados. Se uma tabela que está sendo descartada fizer referência à chave primária de outra tabela que também está sendo descartada, a tabela de referência com a chave estrangeira deverá ser listada antes da tabela que contém a chave primária que está sendo referenciada.  
  
 Quando uma tabela for descartada, as regras ou os padrões da tabela perderão sua associação e quaisquer restrições ou gatilhos associados à tabela serão descartados automaticamente. Se você recriar uma tabela, deverá associar novamente as regras e padrões apropriados, recriar quaisquer gatilhos e adicionar todas as restrições necessárias.  
  
 Se você excluir todas as linhas em uma tabela usando DELETE *tablename* ou usar a instrução TRUNCATE TABLE, a tabela existe até que ela seja descartada.  
  
 Tabelas e índices grandes que usem mais de 128 extensões são descartados em duas fases separadas: a fase lógica e a física. Na fase lógica, as unidades de alocação existentes usadas pela tabela são marcadas para desalocação e bloqueadas até que a transação seja confirmada. Na fase física, as páginas IAM marcadas para desalocação são descartadas fisicamente em lotes.  
  
 Se você descartar uma tabela que contém uma coluna VARBINARY(MAX) com o atributo FILESTREAM, os dados armazenados no sistema de arquivos não serão removidos.  
  
> [!IMPORTANT]  
>  DROP TABLE e CREATE TABLE não devem ser executados na mesma tabela no mesmo lote. Caso contrário, poderá ocorrer um erro inesperado.  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão ALTER no esquema ao qual a tabela pertence, permissão CONTROL na tabela ou associação na função de banco de dados fixa **db_ddladmin** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-dropping-a-table-in-the-current-database"></a>A. Descartando uma tabela no banco de dados atual  
 O exemplo a seguir remove a tabela `ProductVendor1` e seus dados e índices do banco de dados atual.  
  
```  
DROP TABLE ProductVendor1 ;  
```  
  
### <a name="b-dropping-a-table-in-another-database"></a>B. Descartando uma tabela em outro banco de dados  
 O exemplo a seguir descarta a tabela `SalesPerson2` no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. O exemplo pode ser executado a partir de qualquer banco de dados na instância do servidor.  
  
```  
DROP TABLE AdventureWorks2012.dbo.SalesPerson2 ;  
```  
  
### <a name="c-dropping-a-temporary-table"></a>C. Descartando uma tabela temporária  
 O exemplo a seguir cria uma tabela temporária, testa sua existência, descarta a mesma e testa novamente sua existência. Este exemplo não usa o **IF EXISTS** sintaxe que está disponível a partir [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
```  
CREATE TABLE #temptable (col1 int);  
GO  
INSERT INTO #temptable  
VALUES (10);  
GO  
SELECT * FROM #temptable;  
GO  
IF OBJECT_ID(N'tempdb..#temptable', N'U') IS NOT NULL   
DROP TABLE #temptable;  
GO  
--Test the drop.  
SELECT * FROM #temptable;  
  
```  
  
### <a name="d-dropping-a-table-using-if-exists"></a>D. Descartando uma tabela usando IF EXISTS  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 O exemplo a seguir cria uma tabela nomeada T1. Em seguida, a segunda instrução descarta a tabela. A terceira instrução não realiza nenhuma ação porque a tabela já foi excluída, mas não causa um erro.  
  
```  
CREATE TABLE T1 (Col1 int);  
GO  
DROP TABLE IF EXISTS T1;  
GO  
DROP TABLE IF EXISTS T1;  
```  
  
  
## <a name="see-also"></a>Consulte também  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [TRUNCATE TABLE &#40; Transact-SQL &#41;](../../t-sql/statements/truncate-table-transact-sql.md)   
 [DROP VIEW &#40; Transact-SQL &#41;](../../t-sql/statements/drop-view-transact-sql.md)   
 [DROP PROCEDURE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-procedure-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
