---
description: sp_data_source_objects (Transact-SQL)
title: sp_data_source_objects | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sp_data_source_objects
helpviewer_keywords:
- PolyBase
ms.assetid: 48066431-fed2-4a8a-85af-ac704689e183
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: d30a5190d88a0b3714f670f5f253c2a31e98f69e
ms.sourcegitcommit: 2e7154475ba1f31d1aeebc8f48ac05846f793736
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126602"
---
# <a name="sp_data_source_objects-transact-sql"></a>sp_data_source_objects (Transact-SQL)

[!INCLUDE [sqlserver2019](../../includes/applies-to-version/sqlserver2019.md)]

Retorna a lista de objetos de tabela que estão disponíveis para serem virtualizados.

> [!NOTE]
> Esse procedimento é introduzido no [SQL 2019 CU5](../../big-data-cluster/release-notes-big-data-cluster.md#cu5).

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

## <a name="syntax"></a>Sintaxe  

```syntaxsql
sp_data_source_objects  
         [ @data_source = ] 'data_source'
     [ , [ @object_root_name = ] 'object_root_name' ]
     [ , [ @max_search_depth = ] max_search_depth ]
     [ , [ @search_options = ] 'search_options' ]
[ ; ]
```  
  
## <a name="arguments"></a>Argumentos  

`[ @data_source = ] 'data_source'`   
O nome da fonte de dados externa da qual obter os metadados. `@data_source` é `sysname`.  

`[ @object_root_name = ] 'object_root_name'`   
Esse parâmetro é a raiz do nome dos objetos a serem pesquisados. `@object_root_name` é `nvarchar(max)` , com um padrão de `NULL` .

Essa chamada só retorna objetos externos que começam com o valor definido para `@object_root_name` .

Se uma fonte de dados ODBC se conecta a um RDBMS (sistema de gerenciamento de banco de dados relacional) que usa nomes de três partes, `@object_root_name` não pode conter um nome de banco de dados parcial. Nesses casos, o parâmetro `@object_root_name` deve conter todas as três partes, com a terceira parte sendo o nome do objeto a ser pesquisado.
> [!CAUTION]
> Devido a diferenças entre plataformas de dados externos, algumas plataformas não retornarão resultados se o valor padrão de `NULL` for fornecido. Alguns tratados `NULL` como a falta de um filtro. Por exemplo, o Oracle RDBMS não retornará resultados se `NULL` for fornecido para `@object_root_name` .

`[ @max_search_depth = ] max_search_depth`   
Esse valor especifica a profundidade máxima (em partes) `@object_root_name` que desejamos Pesquisar. `@max_search_depth` é um `int` com um padrão de 1.

Por exemplo, um `@max_search_depth` de 1, com um `@object_root_name` que é o nome de um banco de dados SQL Server, retornaria Schemata contido no banco de dados.

Um `@max_search_depth` de retornará `NULL` informações sobre `@object_root_name` se ele existe e não está vazio, no caso do catálogo ou do esquema.

`[ @search_options = ] 'search_options'`   
O `search_options` parâmetro é nvarchar (max) com um padrão de `NULL` .

Esse parâmetro não é usado, mas pode ser implementado no futuro.

## <a name="result-sets"></a>Conjuntos de resultados

| Nome da coluna | Tipo de Dados | Descrição |
|--|--|--|
| Object_Type | nvarchar(200) | O tipo do objeto (exemplo: tabela ou banco de dados). |
| OBJECT_NAME | nvarchar(max) | O nome totalmente qualificado do objeto. Escape usando caractere de aspas específica de back-end. |
| OBJECT_LEAF_NAME | nvarchar(max) | O nome do objeto não qualificado. |
| TABLE_LOCATION | nvarchar(max) | Uma cadeia de caracteres de local de tabela válida que poderia ser usada para uma instrução CREATE EXTERNAL TABLE. Será `NULL` se não for aplicável. |
  
## <a name="permissions"></a>Permissões

Requer a permissão ALTER ANY EXTERNAL DATA SOURCE.  

## <a name="remarks"></a>Comentários  

A instância de SQL Server deve ter o recurso  [polybase](../../relational-databases/polybase/polybase-guide.md) instalado.

Este procedimento armazenado dá suporte a conectores para:

- SQL Server
- Oracle
- Teradata
- MongoDB
- CosmosDB

O procedimento armazenado não oferece suporte a conectores de origem ODBC DTA genéricos.

A noção de vazio versus não vazio se relaciona com o comportamento do driver ODBC e da [ `SQLTables` função](../native-client-odbc-api/sqltables.md). Não vazio indica que um objeto contém tabelas, não linhas. Por exemplo, um esquema vazio não contém tabelas no SQL Server. Um banco de dados vazio contém sem tabelas no Teradata.

Os tipos de objeto são determinados pelo driver ODBC da fonte de dados externa. Cada fonte de dados externa determina o que é qualificado como uma tabela. Isso pode incluir objetos de banco de dados como funções em TeraData ou sinônimos no Oracle. O polybase não pode se conectar a alguns objetos ODBC como tabelas externas e, portanto, não terá um valor na coluna TABLE_LOCATION. Apesar disso, a presença de um desses objetos pode tornar um banco de dados ou esquema não vazio.

Use `sp_data_source_objects` e [`sp_data_source_table_columns`](sp-data-source-table-columns.md) para descobrir objetos externos. Esses procedimentos armazenados do sistema retornam o esquema de tabelas que estão disponíveis para serem virtualizadas. O Azure Data Studio usa esses dois procedimentos armazenados para dar suporte à [virtualização de dados](../../azure-data-studio/extensions/data-virtualization-extension.md). Use [sp_data_source_table_columns](sp-data-source-table-columns.md) para descobrir esquemas de tabela externos representados em SQL Server tipos de dados.

### <a name="data-source-type-specific-remarks"></a>Comentários específicos do tipo de fonte de dados

* Teradata

   As exibições do sistema Teradata não usam a RLS (segurança em nível de linha) e, portanto, os usuários podem ver a existência de tabelas que não podem consultar.

* MongoDB

   Algumas versões anteriores do MongoDB restringem a capacidade de listar todos os bancos de dados para usuários do tipo administrador. Os usuários sem essa permissão podem obter erros de autenticação ao tentar executar este procedimento com um valor nulo `@object_root_name` .

## <a name="examples"></a>Exemplos  

### <a name="sql-server"></a>SQL Server

O exemplo a seguir retorna todos os bancos de dados, Schemata e tabelas/exibições

```sql
DECLARE @data_source SYSNAME = N'ExternalDataSourceName';
DECLARE @object_root_name NVARCHAR(MAX) = NULL;
DECLARE @max_search_depth INT = 3;
EXEC sp_data_source_objects @data_source, @object_root_name, @max_search_depth;
```

| Object_Type | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |
|--|--|--|--|
| DATABASE | "database" | Banco de Dados | NULO |
| SCHEMA | "banco de dados". dbo | dbo | NULO |
| TABLE | "banco de dados". dbo "." cliente | cliente | [banco de dados]. [dbo]. cliente |
| TABLE | "banco de dados". dbo "." item | item | [banco de dados]. [dbo]. item |
| TABLE | "banco de dados". dbo "." EUA | EUA | [banco de dados]. [dbo]. EUA |

O exemplo a seguir retorna todos os bancos de dados

```sql
DECLARE @data_source SYSNAME = N'ExternalDataSourceName';
DECLARE @object_root_name NVARCHAR(MAX) = NULL;
EXEC sp_data_source_objects @data_source, @object_root_name;
```

| Object_Type | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |
|--|--|--|--|
| DATABASE | "UserDatabase" | Banco de dados | NULO |
| DATABASE | "master" | master | NULO |
| DATABASE | msdb | msdb | NULO |
| DATABASE | tempdb | tempdb | NULO |
| DATABASE | "database" | Banco de Dados | NULO |

O exemplo a seguir retorna todos os Schemata em um banco de dados

```sql
DECLARE @data_source SYSNAME = N'ExternalDataSourceName'; 
DECLARE @object_root_name NVARCHAR(MAX) = N'[database]'; 
EXEC sp_data_source_objects @data_source, @object_root_name;
```

| Object_Type | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |
|--|--|--|--|
| SCHEMA | "banco de dados". dbo | dbo | NULO |
| SCHEMA | "banco de dados". INFORMATION_SCHEMA " | INFORMATION_SCHEMA | NULO |
| SCHEMA | "banco de dados". sistema | sys | NULO |

O exemplo a seguir retorna todas as tabelas no esquema 

```sql
DECLARE @data_source SYSNAME = N'ExternalDataSourceName'; 
DECLARE @object_root_name NVARCHAR(MAX) = N'[database].[dbo]'; 
EXEC sp_data_source_objects @data_source, @object_root_name;
```

| Object_Type | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |
|--|--|--|--|
| TABLE | "banco de dados". dbo "." cliente | cliente | [banco de dados]. [dbo]. cliente |
| TABLE | "banco de dados". dbo "." item | item | [banco de dados]. [dbo]. item |
| TABLE | "banco de dados". dbo "." EUA | EUA | [banco de dados]. [dbo]. EUA |
| TABLE | "banco de dados". dbo "." solicitar | pedidos | [banco de dados]. [dbo]. solicitar |
| TABLE | "banco de dados". dbo "." parte | Parte | [banco de dados]. [dbo]. parte |

### <a name="oracle"></a>Oracle

O exemplo a seguir retorna o Schemata completo e as tabelas, funções, exibições e etc.

```sql
DECLARE @data_source SYSNAME = N'ExternalDataSourceName'; 
DECLARE @object_root_name NVARCHAR(MAX) = N'[OracleObjectRoot]'; 
DECLARE @max_search_depth INT = 2; 
EXEC sp_data_source_objects @data_source, @object_root_name, @max_search_depth;
```

| Object_Type | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |
|--|--|--|--|
| VIEW | "SYS". ALL_SQLSET_STATEMENTS " | ALL_SQLSET_STATEMENTS | [ORACLEOBJECTROOT]. [SYS]. [ALL_SQLSET_STATEMENTS] |
| SYSTEM TABLE | "SYS". BOOTSTRAP $ " | INICIALIZAÇÃO $ | [ORACLEOBJECTROOT]. [SYS]. [BOOTSTRAP $] |
| SYNONYM | "PÚBLICO". ALL_ALL_TABLES " | ALL_ALL_TABLES | NULO |
| SCHEMA | "database" | Banco de Dados | NULO |
| TABLE | "banco de dados". cliente | cliente | [ORACLEOBJECTROOT]. [banco de dados]. cliente |

### <a name="teradata"></a>Teradata

O exemplo a seguir retorna todos os bancos de dados e tabelas, funções, exibições e etc.

```SQL
DECLARE @data_source SYSNAME = N'ExternalDataSourceName';
DECLARE @object_root_name NVARCHAR(MAX) = NULL;
DECLARE @max_search_depth INT = 2;
EXEC sp_data_source_objects @data_source, @object_root_name, @max_search_depth;
```

| Object_Type | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |  
|--|--|--|--|
| FUNCTION | "SYSLIB"." ExtractRoles" | ExtractRoles | NULO |  
| SYSTEM TABLE | "DBC". UDTCast" | UDTCast | [DBC]. [UDTCast] |  
| TYPE | "SYSUDTLIB"." XML | XML | NULO |  
| DATABASE | "database" | Banco de Dados | NULO |
| TABLE | "banco de dados". cliente | cliente | [banco de dados]. cliente |  

### <a name="mongo-db"></a>Mongo DB

O exemplo a seguir retorna todos os bancos de dados e tabelas.

```SQL
DECLARE @data_source SYSNAME = N'ExternalDataSourceName';
DECLARE @object_root_name NVARCHAR(MAX) = NULL;
DECLARE @max_search_depth INT = 2;
EXEC sp_data_source_objects @data_source, @object_root_name, @max_search_depth;
```

| Object_Type | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |
|--|--|--|--|
| DATABASE | "database" | Banco de Dados | NULO |
| TABLE | "banco de dados". cliente | cliente | [banco de dados]. cliente |
| TABLE | "banco de dados". item | item | [banco de dados]. item |
| TABLE | "banco de dados". EUA | EUA | [banco de dados]. EUA |
| TABLE | "banco de dados". solicitar | pedidos | [banco de dados]. solicitar |

## <a name="see-also"></a>Consulte também

- [sp_data_source_columns](/sql/relational-databases/system-stored-procedures/sp-data-source-table-columns)   
- [CREATE EXTERNAL TABLE AS SELECT (Transact-SQL)](../../t-sql/statements/create-external-table-as-select-transact-sql.md)
- [CREATE EXTERNAL TABLE (Transact-SQL)](../../t-sql/statements/create-external-table-transact-sql.md)
- [Extensão Virtualização de Dados para o Azure Data Studio](../../azure-data-studio/extensions/data-virtualization-extension.md)   
- [Introdução ao PolyBase](../polybase/polybase-guide.md)   
- [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)
