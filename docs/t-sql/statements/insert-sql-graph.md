---
title: "INSERT (gráfico SQL) | Microsoft Docs"
description: "Insira a sintaxe para tabelas de borda ou nó de gráfico de SQL."
ms.date: 05/12/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- INSERT statement [SQL Server], SQL graph
- SQL graph, INSERT statement
ms.assetid: 
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e694d89efef130d2abcd5cd6424e2be576ef09de
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---

# <a name="insert-sql-graph"></a>INSERT (gráfico SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]  

  Adiciona uma ou mais linhas para uma `node` ou `edge` tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 

> [!NOTE]   
>  Para instruções de Transact-SQL padrão, consulte [Inserir tabela (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md).
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="insert-into-node-table-syntax"></a>Insira a sintaxe de tabela do nó 
A sintaxe para inserção em uma tabela de nó é o mesma que uma tabela normal. 

```  
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
 Este documento descreve os argumentos relativos ao gráfico SQL. Para uma lista completa e a descrição de argumentos com suporte na instrução INSERT, consulte [Inserir tabela (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)

 INTO  
 É uma palavra-chave opcional que pode ser usada entre `INSERT` e a tabela de destino.  
  
 *search_condition_with_match*   
 `MATCH`cláusula pode ser usada em uma subconsulta ao inserir em uma tabela de borda ou nó. Para `MATCH` sintaxe de instrução, consulte [correspondência de gráfico (Transact-SQL)](../../t-sql/queries/match-sql-graph.md)

 *graph_search_pattern*   
 Padrão de pesquisa fornecido para `MATCH` cláusula como parte do predicado de gráfico.

 *edge_table_column_list*   
 Os usuários devem fornecer valores para `$from_id` e `$to_id` ao inserir em uma borda. Um erro será retornado se não for fornecido um valor ou valores nulos são inseridos nessas colunas. 
  

## <a name="remarks"></a>Comentários  
Inserindo um nó é igual ao inserir em qualquer tabela relacional. Valores da coluna $node_id são gerados automaticamente.

Ao inserir em uma tabela de borda, os usuários devem fornecer valores para `$from_id` e `$to_id` colunas.   

Inserção em MASSA para a tabela de nó é permanece igual de uma tabela relacional.

Antes de inserção em uma tabela de borda em massa, as tabelas de nó devem ser importadas. Os valores para `$from_id` e `$to_id` , em seguida, pode ser extraído do `$node_id` coluna da tabela de nó e inseridos como bordas. 

  
### <a name="permissions"></a>Permissões  
 A permissão INSERT é necessária na tabela de destino.  
  
 Inserir as permissões padrão para membros do **sysadmin** função de servidor fixa, o **db_owner** e **db_datawriter** fixo de funções de banco de dados e o proprietário da tabela. Membros de **sysadmin**, **db_owner**e o **db_securityadmin** funções e o proprietário da tabela podem transferir permissões a outros usuários.  
  
 Para executar INSERT com a opção BULK da função OPENROWSET, você deve ser um membro do **sysadmin** função fixa de servidor ou o **bulkadmin** função de servidor fixa.  
  

## <a name="examples"></a>Exemplos  
  
#### <a name="a--insert-into-node-table"></a>A.  Inserir tabela do nó  
 O exemplo a seguir cria uma tabela de nó de pessoa e insere 2 linhas na tabela.

 ```
 -- Create person node table
 CREATE TABLE dbo.Person (ID integer PRIMARY KEY, name varchar(50)) AS NODE;
 
 -- Insert records for Alice and John
 INSERT INTO dbo.Person VALUES (1, 'Alice');
 INSERT INTO dbo.Person VALUES (2,'John');
 ```
  
#### <a name="b--insert-into-edge-table"></a>B.  Inserir tabela de borda  
 O exemplo a seguir cria uma tabela de borda de amigo e insere uma borda na tabela.

 ```
 -- Create friend edge table
 CREATE TABLE dbo.friend (start_date DATE) AS EDGE;

 -- Create a friend edge, that connect Alice and John
 INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'Alice'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'John'), '9/15/2011');
 ```

  
## <a name="see-also"></a>Consulte também  
 [Inserir tabela &#40; Transact-SQL &#41;](../../t-sql/statements/insert-transact-sql.md)   
 [Gráfico de processamento com o SQL Server 2017](../../relational-databases/graphs/sql-graph-overview.md)  



