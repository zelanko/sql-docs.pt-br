---
title: "Criar tabela (SQL gráfico) | Microsoft Docs"
ms.custom: 
ms.date: 05/04/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
ms.assetid: 
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c32a8c4f683f20c4384089c1d2552614090f9b3d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---

# <a name="create-table-sql-graph"></a>Criar tabela (gráfico SQL)
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]   

Cria uma nova tabela de gráfico do SQL como uma `NODE` ou um `EDGE` tabela. 
  
> [!NOTE]   
>  Para instruções de Transact-SQL padrão, consulte [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md).
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
CREATE TABLE   
    [ database_name . [ schema_name ] . | schema_name . ] table_name   
    ( { <column_definition> } [ ,...n ] )   
    AS [ NODE | EDGE ]
[ ; ]  
```  
  
  
## <a name="arguments"></a>Argumentos  
Este documento lista apenas os argumentos que pertencem ao gráfico SQL. Para uma lista completa e a descrição de argumentos com suporte, consulte [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)

 *Database_Name*    
 É o nome do banco de dados no qual a tabela é criada. *Database_Name* deve especificar o nome do banco de dados existente. Se não for especificado, *database_name* padrões para o banco de dados atual. O logon para a conexão atual deve ser associado uma ID de usuário existente no banco de dados especificado por *database_name*, e essa ID de usuário deve ter permissões CREATE TABLE.  
  
 *schema_name*    
 É o nome do esquema ao qual a nova tabela pertence.  
  
 *table_name*    
 É o nome da tabela de borda ou nó. Nomes de tabela devem seguir as regras para [identificadores](../../relational-databases/databases/database-identifiers.md). *table_name* pode ter no máximo 128 caracteres, exceto para nomes de tabelas temporárias locais (nomes prefixados com um único sinal numérico (#)) que não podem exceder 116 caracteres.  
  
 NÓ   
 Cria uma tabela de nó.

 BORDA  
 Cria uma tabela de borda.  
  
## <a name="remarks"></a>Comentários  
Não há suporte para a criação de uma tabela temporária como nó ou a tabela de borda.  

Não há suporte para a criação de uma tabela de borda ou nó como uma tabela temporal.

Não há suporte para o Stretch database para a tabela de borda ou nó.

Tabelas de borda ou o nó não podem ser tabelas externas (sem suporte do polybase para tabelas de gráfico). 
  
 
## <a name="examples"></a>Exemplos  
  
### <a name="a-create-a-node-table"></a>A. Criar um `NODE` tabela
 O exemplo a seguir mostra como criar um `NODE` tabela

```
 CREATE TABLE Person (
        ID INTEGER PRIMARY KEY, 
        name VARCHAR(100), 
        email VARCHAR(100)
 ) AS NODE;
```

### <a name="b-create-an-edge-table"></a>B. Criar um `EDGE` tabela
Os exemplos a seguir mostram como criar `EDGE` tabelas

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


## <a name="see-also"></a>Consulte também  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [INSERT (gráfico SQL)](../../t-sql/statements/insert-sql-graph.md)]  
 [Gráfico de processamento com o SQL Server 2017](../../relational-databases/graphs/sql-graph-overview.md)


