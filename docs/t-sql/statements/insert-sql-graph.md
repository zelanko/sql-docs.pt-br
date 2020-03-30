---
title: INSERT (SQL Graph) | Microsoft Docs
description: Sintaxe de INSERT para tabelas de borda ou nó do SQL Graph.
ms.date: 05/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.custom: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- INSERT statement [SQL Server], SQL graph
- SQL graph, INSERT statement
ms.assetid: ''
author: shkale-msft
ms.author: shkale
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8c4cfba19dc16e043ba6325fb6c9acb1665a597f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68071167"
---
# <a name="insert-sql-graph"></a>INSERT (SQL Graph)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Adiciona uma ou mais linhas a uma tabela `node` ou `edge` do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 

> [!NOTE]   
>  Para obter instruções Transact-SQL padrão, consulte [INSERT TABLE (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md).
  
![Ícone de link do artigo](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do artigo") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="insert-into-node-table-syntax"></a>Sintaxe de INSERT na tabela Node 
A sintaxe para inserção em uma tabela Node é a mesma de uma tabela normal. 

```sql
[ WITH <common_table_expression> [ ,...n ] ]  
INSERT   
{  
        [ TOP ( expression ) [ PERCENT ] ]   
        [ INTO ]   
        { <object> | rowset_function_limited   
          [ WITH ( <Table_Hint_Limited> [ ...n ] ) ]  
        }  
    {  
        [ (column_list) ] | [(<edge_table_column_list>)]  
        [ <OUTPUT Clause> ]  
        { VALUES ( { DEFAULT | NULL | expression } [ ,...n ] ) [ ,...n     ]   
        | derived_table   
        | execute_statement  
        | <dml_table_source>  
        | DEFAULT VALUES   
        }  
    }  
}  
[;]  
  
<object> ::=  
{   
    [ server_name . database_name . schema_name .   
      | database_name .[ schema_name ] .   
      | schema_name .   
    ]  
    node_table_name  | edge_table_name
}  
  
<dml_table_source> ::=  
    SELECT <select_list>  
    FROM ( <dml_statement_with_output_clause> )   
      [AS] table_alias [ ( column_alias [ ,...n ] ) ]  
    [ WHERE <on_or_where_search_condition> ]  
        [ OPTION ( <query_hint> [ ,...n ] ) ]  

<on_or_where_search_condition> ::=
    {  <search_condition_with_match> | <search_condition> }

<search_condition_with_match> ::=
    { <graph_predicate> | [ NOT ] <predicate> | ( <search_condition> ) }
    [ AND { <graph_predicate> | [ NOT ] <predicate> | ( <search_condition> ) } ]
    [ ,...n ]

<search_condition> ::=
    { [ NOT ] <predicate> | ( <search_condition> ) }
    [ { AND | OR } [ NOT ] { <predicate> | ( <search_condition> ) } ]
    [ ,...n ]

<graph_predicate> ::=
    MATCH( <graph_search_pattern> [ AND <graph_search_pattern> ] [ , ...n] )

<graph_search_pattern>::=
    <node_alias> { { <-( <edge_alias> )- | -( <edge_alias> )-> } <node_alias> }

<edge_table_column_list> ::=
    ($from_id, $to_id, [column_list])

```  
  
 
## <a name="arguments"></a>Argumentos  
Este documento descreve os argumentos relativos ao SQL Graph. Para obter uma lista completa e a descrição de argumentos compatíveis com a instrução INSERT, consulte [INSERT TABLE (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)

INTO  
É uma palavra-chave opcional que pode ser usada entre `INSERT` e a tabela de destino.  
  
*search_condition_with_match*   
A cláusula `MATCH` pode ser usada em uma subconsulta durante a inserção em uma tabela de borda ou nó. Para obter a sintaxe da instrução `MATCH`, consulte [GRAPH MATCH (Transact-SQL)](../../t-sql/queries/match-sql-graph.md)

*graph_search_pattern*   
Padrão de pesquisa fornecido para a cláusula `MATCH` como parte do predicado de gráfico.

*edge_table_column_list*   
Os usuários devem fornecer valores para `$from_id` e `$to_id` ao fazer uma inserção em uma borda. Um erro será retornado se não um valor não for fornecido ou se valores NULL forem inseridos nessas colunas. 
  

## <a name="remarks"></a>Comentários  
A inserção em um nó é igual à inserção em qualquer tabela relacional. Os valores da coluna $node_id são gerados automaticamente.

Ao fazer uma inserção em uma tabela de borda, os usuários devem fornecer valores para as colunas `$from_id` e `$to_id`.   

A BULK INSERT para a tabela de nó é a mesma que a de uma tabela relacional.

Antes da inserção em massa em uma tabela de borda, as tabelas de nó devem ser importadas. Em seguida, os valores para `$from_id` e `$to_id` podem ser extraídos da coluna `$node_id` da tabela de nó e inseridos como bordas. 

  
### <a name="permissions"></a>Permissões  
A permissão INSERT é necessária na tabela de destino.  
  
As permissões INSERT usam como padrão os membros da função de servidor fixa **sysadmin**, as funções de banco de dados fixa **db_owner** e **db_datawriter** e o proprietário da tabela. Os membros das funções **sysadmin**, **db_owner** e **db_securityadmin** e o proprietário da tabela podem transferir permissões para outros usuários.  
  
Para executar INSERT com a opção BULK da função OPENROWSET, você precisa ser membro da função de servidor fixa **sysadmin** ou **bulkadmin**.  
  

## <a name="examples"></a>Exemplos  
  
#### <a name="a--insert-into-node-table"></a>a.  Inserir na tabela de nó  
O exemplo a seguir cria uma tabela de nó Person e insere duas linhas nessa tabela.

```sql
-- Create person node table
CREATE TABLE dbo.Person (ID integer PRIMARY KEY, name varchar(50)) AS NODE;
 
-- Insert records for Alice and John
INSERT INTO dbo.Person VALUES (1, 'Alice');
INSERT INTO dbo.Person VALUES (2,'John');
```
  
#### <a name="b--insert-into-edge-table"></a>B.  Inserir na tabela de borda  
O exemplo a seguir cria uma tabela de borda de amigo e insere uma borda na tabela.

```sql
-- Create friend edge table
CREATE TABLE dbo.friend (start_date DATE) AS EDGE;

-- Create a friend edge, that connect Alice and John
INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'Alice'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'John'), '9/15/2011');
```

  
## <a name="see-also"></a>Consulte Também  
[INSERT TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
[Processamento de grafo com o SQL Server 2017](../../relational-databases/graphs/sql-graph-overview.md)  


