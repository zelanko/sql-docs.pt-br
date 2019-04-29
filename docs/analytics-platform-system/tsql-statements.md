---
title: Instruções T-SQL - Parallel Data Warehouse | Microsoft Docs
description: Instruções T-SQL para análise Platform System (APS) SQL Server Parallel Data Warehouse (PDW).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: ca12b3926fb848defc2a19a08ffa9702516726fd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63034933"
---
# <a name="t-sql-statements-for-parallel-data-warehouse"></a>Instruções T-SQL para Parallel Data Warehouse
Instruções de Transact-SQL (T-SQL) para análise Platform System (APS) SQL Server Parallel Data Warehouse (PDW).

## <a name="data-definition-language-ddl-statements"></a>Instruções de Definition Language (DDL) de dados
* [ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)
* [ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md)
* [ALTER PROCEDURE](../t-sql/statements/alter-procedure-transact-sql.md)
* [ALTER SCHEMA](../t-sql/statements/alter-schema-transact-sql.md)
* [ALTER TABLE](../t-sql/statements/alter-table-transact-sql.md)
* [CREATE COLUMNSTORE INDEX](../t-sql/statements/create-columnstore-index-transact-sql.md)
* [CREATE DATABASE](../t-sql/statements/create-database-azure-sql-data-warehouse.md)
* [CRIAR BANCO DE DADOS COM ESCOPO DE CREDENCIAL](../t-sql/statements/create-database-scoped-credential-transact-sql.md)
* [CRIAR FONTE DE DADOS EXTERNA](../t-sql/statements/create-external-data-source-transact-sql.md)
* [CRIAR FORMATO DE ARQUIVO EXTERNO](../t-sql/statements/create-external-file-format-transact-sql.md)
* [CRIAR TABELA EXTERNA](../t-sql/statements/create-external-table-transact-sql.md)
* [CRIAR FUNÇÃO](../t-sql/statements/create-function-sql-data-warehouse.md)
* [CREATE INDEX](../t-sql/statements/create-index-transact-sql.md)
* [CREATE PROCEDURE](../t-sql/statements/create-procedure-transact-sql.md)
* [CRIAR ESQUEMA](../t-sql/statements/create-schema-transact-sql.md)
* [CREATE STATISTICS](../t-sql/statements/create-statistics-transact-sql.md)
* [CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md)
* [CREATE TABLE AS SELECT](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)
* [CREATE VIEW](../t-sql/statements/create-view-transact-sql.md)
* [REMOVER FONTE DE DADOS EXTERNA](../t-sql/statements/drop-external-data-source-transact-sql.md)
* [REMOVER O FORMATO DE ARQUIVO EXTERNO](../t-sql/statements/drop-external-file-format-transact-sql.md)
* [REMOVER TABELA EXTERNA](../t-sql/statements/drop-external-table-transact-sql.md)
* [DROP INDEX](../t-sql/statements/drop-index-transact-sql.md)
* [PROCEDIMENTO DE DESCARTE](../t-sql/statements/drop-procedure-transact-sql.md)
* [REMOVER ESTATÍSTICAS](../t-sql/statements/drop-statistics-transact-sql.md)
* [DROP TABLE](../t-sql/statements/drop-table-transact-sql.md)
* [DROP SCHEMA](../t-sql/statements/drop-schema-transact-sql.md)
* [REMOVER EXIBIÇÃO](../t-sql/statements/drop-view-transact-sql.md)
* [RENAME](../t-sql/statements/rename-transact-sql.md)
* [TRUNCATE TABLE](../t-sql/statements/truncate-table-transact-sql.md)
* [UPDATE STATISTICS](../t-sql/statements/update-statistics-transact-sql.md)

## <a name="data-manipulation-language-dml-statements"></a>Instruções de manipulação DML (linguagem) de dados
* [DELETE](../t-sql/statements/delete-transact-sql.md)
* [INSERT](../t-sql/statements/insert-transact-sql.md)
* [UPDATE](../t-sql/queries/update-transact-sql.md)

## <a name="database-console-commands"></a>Comandos de Console de Banco de Dados
* [DBCC DROPCLEANBUFFERS](../t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql.md)
* [DBCC FREEPROCCACHE](https://msdn.microsoft.com/library/mt204018.aspx)
* [DBCC SHRINKLOG](https://msdn.microsoft.com/library/mt204020.aspx)
* [DBCC PDW_SHOWEXECUTIONPLAN](https://msdn.microsoft.com/library/mt204017.aspx)
* [DBCC PDW_SHOWPARTITIONSTATS](https://msdn.microsoft.com/library/mt204013.aspx)
* [DBCC PDW_SHOWSPACEUSED](../t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql.md)
* [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/mt204043.aspx)

## <a name="query-statements"></a>Instruções de consulta
* [SELECT](../t-sql/queries/select-transact-sql.md)
* [WITH common_table_expression](../t-sql/queries/with-common-table-expression-transact-sql.md)
* [EXCEPT e INTERSECT](../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)
* [EXPLAIN](../t-sql/queries/explain-transact-sql.md)
* [FROM](../t-sql/queries/from-transact-sql.md)
* [Usando PIVOT e UNPIVOT](../t-sql/queries/from-using-pivot-and-unpivot.md)
* [GROUP BY](../t-sql/queries/select-group-by-transact-sql.md)
* [HAVING](../t-sql/queries/select-having-transact-sql.md)
* [ORDER BY](../t-sql/queries/select-order-by-clause-transact-sql.md)
* [OPTION](../t-sql/queries/option-clause-transact-sql.md)
* [UNION](../t-sql/language-elements/set-operators-union-transact-sql.md)
* [WHERE](../t-sql/queries/where-transact-sql.md)
* [TOP](../t-sql/queries/top-transact-sql.md)
* [Aliasing](../t-sql/queries/aliasing-azure-sql-data-warehouse-parallel-data-warehouse.md)
* [Critério de pesquisa](../t-sql/queries/search-condition-transact-sql.md)
* [Subconsultas](../t-sql/queries/subqueries-azure-sql-data-warehouse-parallel-data-warehouse.md)

## <a name="security-statements"></a>Instruções de segurança
* Permissões: [GRANT](../t-sql/statements/grant-transact-sql.md), [DENY](../t-sql/statements/deny-transact-sql.md), [REVOKE](../t-sql/statements/revoke-transact-sql.md)
* [ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md)
* [ALTERAR CERTIFICADO](../t-sql/statements/alter-certificate-transact-sql.md)
* [ALTERAR CHAVE DE CRIPTOGRAFIA DE BANCO DE DADOS](../t-sql/statements/alter-database-encryption-key-transact-sql.md)
* [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md)
* [ALTER MASTER KEY](../t-sql/statements/alter-master-key-transact-sql.md)
* [ALTERAR FUNÇÃO](../t-sql/statements/alter-role-transact-sql.md)
* [ALTERAR USUÁRIO](../t-sql/statements/alter-user-transact-sql.md)
* [BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)
* [CLOSE MASTER KEY](../t-sql/statements/close-master-key-transact-sql.md)
* [CRIAR CERTIFICADO](../t-sql/statements/create-certificate-transact-sql.md)
* [CRIAR CHAVE DE CRIPTOGRAFIA DE BANCO DE DADOS](../t-sql/statements/create-database-encryption-key-transact-sql.md)
* [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md)
* [CREATE MASTER KEY](../t-sql/statements/create-master-key-transact-sql.md)
* [CRIAR FUNÇÃO](../t-sql/statements/create-role-transact-sql.md)
* [CRIAR USUÁRIO](../t-sql/statements/create-user-transact-sql.md)
* [REMOVER CERTIFICADO](../t-sql/statements/drop-certificate-transact-sql.md)
* [DROP DATABASE ENCRYPTION KEY](../t-sql/statements/drop-database-encryption-key-transact-sql.md)
* [DROP LOGIN](../t-sql/statements/drop-login-transact-sql.md)
* [DROP MASTER KEY](../t-sql/statements/drop-master-key-transact-sql.md)
* [REMOVER FUNÇÃO](../t-sql/statements/drop-role-transact-sql.md)
* [DESCARTE O USUÁRIO](../t-sql/statements/drop-user-transact-sql.md)
* [OPEN MASTER KEY](../t-sql/statements/open-master-key-transact-sql.md)

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações de referência, consulte [elementos de linguagem T-SQL](tsql-language-elements.md) e [exibições do sistema T-SQL](tsql-system-views.md).

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
