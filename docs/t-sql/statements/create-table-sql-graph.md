---
title: CREATE TABLE (SQL Graph) | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SQL_GRAPH_TSQL
- TABLE
- CREATE_TABLE_TSQL
- NODE
- NODE_TSQL
- AS_NODE
- AS_NODE_TSQL
- EDGE
- EDGE_TSQL
- AS_EDGE
- AS_EDGE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- graph
- SQL graph
- CREATE TABLE SQL graph
- NODE
- EDGE
- SQL graph, CREATE TABLE statement
ms.assetid: ''
author: shkale-msft
ms.author: shkale
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 37e374d44fc6013c1cdf6b9594d709ff4282f7aa
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70846716"
---
# <a name="create-table-sql-graph"></a>CREATE TABLE (SQL Graph)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Cria uma nova tabela do SQL Graph como uma tabela de `NODE` ou de `EDGE`. 
  
> [!NOTE]   
>  Para obter as instruções Transact-SQL padrão, confira [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md).
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
CREATE TABLE   
    { database_name.schema_name.table_name | schema_name.table_name | table_name }
    ( { <column_definition> } 
       | <computed_column_definition>
       | <column_set_definition>
       | [ <table_constraint> ] [ ,... n ]
       | [ <table_index> ] }
          [ ,...n ]
    )   
    AS [ NODE | EDGE ]
    [ ON { partition_scheme_name ( partition_column_name )
           | filegroup
           | "default" } ]
[ ; ] 

< table_constraint > ::=
[ CONSTRAINT constraint_name ]
{
    { PRIMARY KEY | UNIQUE }
        [ CLUSTERED | NONCLUSTERED ]
        (column [ ASC | DESC ] [ ,...n ] )
        [
            WITH FILLFACTOR = fillfactor
           |WITH ( <index_option> [ , ...n ] )
        ]
        [ ON { partition_scheme_name (partition_column_name)
            | filegroup | "default" } ]
    | FOREIGN KEY
        ( column [ ,...n ] )
        REFERENCES referenced_table_name [ ( ref_column [ ,...n ] ) ]
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]
        [ NOT FOR REPLICATION ]
    | CONNECTION
        ( { node_table TO node_table } 
          [ , {node_table TO node_table }]
          [ , ...n ]
        )
        [ ON DELETE { NO ACTION | CASCADE } ]
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )
```  
  
  
## <a name="arguments"></a>Argumentos  
Este documento lista apenas os argumentos que pertencem ao SQL Graph. Para obter uma lista completa e a descrição dos argumentos com suporte, confira [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)

 *database_name*    
 É o nome do banco de dados no qual a tabela é criada. *database_name* precisa especificar o nome de um banco de dados existente. Caso não seja especificado, *database_name* usará o banco de dados atual como padrão. O logon para a conexão atual precisa estar associado a uma ID de usuário existente no banco de dados especificado por *database_name*, e essa ID de usuário precisa ter permissões CREATE TABLE.  
  
 *schema_name*    
 É o nome do esquema ao qual a nova tabela pertence.  
  
 *table_name*      
 É o nome da tabela de borda ou de nó. Os nomes de tabela precisam seguir as regras para [identificadores](../../relational-databases/databases/database-identifiers.md). *table_name* pode ter no máximo 128 caracteres, exceto para nomes de tabelas temporárias locais [nomes com o prefixo de sinal numérico (#)], que não podem exceder 116 caracteres.  
  
 NODE   
 Cria uma tabela de nó.

 EDGE  
 Cria uma tabela de borda.  
 
 *table_constraint*   
 Especifica as propriedades de uma restrição PRIMARY KEY, UNIQUE, FOREIGN KEY, CONNECTION ou CHECK ou uma definição DEFAULT adicionada a uma tabela
 
 ON { partition_scheme | filegroup | "default" }    
 Especifica o esquema de partição ou grupo de arquivos no qual a tabela é armazenada. Se partition_scheme for especificado, a tabela será uma tabela particionada cujas partições são armazenadas em um conjunto de um ou mais grupos de arquivos especificados em partition_scheme. Se filegroup for especificado, a tabela será armazenada no grupo de arquivos nomeado. O grupo de arquivos deve existir no banco de dados. Se "default" é especificado ou se ON não é especificado, a tabela é armazenada no grupo de arquivos padrão. O mecanismo de armazenamento de uma tabela como especificado em CREATE TABLE não pode ser alterado posteriormente.

 ON {partition_scheme | filegroup | "default"}    
 Também pode ser especificado em uma restrição PRIMARY KEY ou UNIQUE. Essas restrições criam índices. Se filegroup for especificado, o índice será armazenado no grupo de arquivos nomeado. Se "default" é especificado ou se ON não é especificado, o índice é armazenado no mesmo grupo de arquivos da tabela. Se a restrição PRIMARY KEY ou UNIQUE criar um índice clusterizado, as páginas de dados da tabela serão armazenadas no mesmo grupo de arquivos que o índice. Se CLUSTERED for especificado ou se a restrição, de outro modo, criar um índice clusterizado e for especificado um partition_scheme diferente do partition_scheme ou do filegroup da definição da tabela ou vice-versa, somente a definição da restrição será respeitada, sendo as demais ignoradas.
  
## <a name="remarks"></a>Remarks  
Não há suporte para a criação de uma tabela temporária como uma tabela de nó ou de borda.  

Não há suporte para a criação de uma tabela de borda ou de nó como uma tabela temporal.

O Stretch Database não é compatível com a tabela de borda ou de nó.

As tabelas de borda ou de nó não podem ser tabelas externas (o PolyBase não dá suporte para tabelas de grafo). 

Uma tabela de borda/nó de grafo não particionada não pode ser alterada para uma tabela de borda/nó de grafo particionada. 
  
 
## <a name="examples"></a>Exemplos  
  
### <a name="a-create-a-node-table"></a>A. Criar uma tabela de `NODE`
 O exemplo a seguir mostra como criar uma tabela de `NODE`

```
 CREATE TABLE Person (
        ID INTEGER PRIMARY KEY, 
        name VARCHAR(100), 
        email VARCHAR(100)
 ) AS NODE;
```

### <a name="b-create-an-edge-table"></a>B. Criar uma tabela de `EDGE`
Os exemplos a seguir mostram como criar tabelas de `EDGE`

```
 CREATE TABLE friends (
    id integer PRIMARY KEY,
    start_date date
 ) AS EDGE;

```

```
 -- Create a likes edge table, this table does not have any user defined attributes   
 CREATE TABLE likes AS EDGE;

```


## <a name="see-also"></a>Consulte Também 
 [ALTER TABLE table_constraint](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [INSERT (SQL Graph)](../../t-sql/statements/insert-sql-graph.md)]  
 [Processamento de grafo com o SQL Server 2017](../../relational-databases/graphs/sql-graph-overview.md)

