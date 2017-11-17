---
title: "CORRESPONDÊNCIA (gráfico SQL) | Microsoft Docs"
ms.custom: 
ms.date: 05/05/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- MATCH
- MATCH_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MATCH statement [SQL Server], SQL graph
- SQL graph, MATCH statement
ms.assetid: 
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: db211fa0988f2dbe6a72291f898d670d44d3f215
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="match-transact-sql"></a>CORRESPONDÊNCIA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

  Especifica um critério de pesquisa para um gráfico. CORRESPONDÊNCIA pode ser usada apenas com as tabelas de nó e borda gráfico, na instrução SELECT como parte da cláusula WHERE. 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
MATCH (<graph_search_pattern>)

<graph_search_pattern>::=
    {<node_alias> { 
                     { <-( <edge_alias> )- } 
                   | { -( <edge_alias> )-> }
                 <node_alias> 
                 } 
     }
     [ { AND } { ( <graph_search_pattern> ) } ]
     [ ,...n ]
  
<node_alias> ::=
    node_table_name | node_alias 

<edge_alias> ::=
    edge_table_name | edge_alias
```

## <a name="arguments"></a>Argumentos  
*graph_search_pattern*  
Especifica o padrão para pesquisar ou o caminho para percorrer o gráfico. Esse padrão usa a sintaxe de arte ASCII Transpor um caminho no gráfico. O padrão varia de um nó para outro por meio de uma borda, na direção da seta fornecida. Borda nomes ou aliases são fornecidos em parantheses. Nomes de nó ou aliases aparecem nas duas extremidades da seta. A seta pode ficar em qualquer direção no padrão.

*node_alias*  
Nome ou alias de uma tabela de nó fornecida na cláusula FROM.

*edge_alias*  
Nome ou alias de uma tabela de borda fornecida na cláusula FROM.


## <a name="remarks"></a>Comentários  
Os nomes de nó dentro de correspondência podem ser repetidos.  Em outras palavras, um nó pode ser percorridos um número arbitrário de vezes na mesma consulta.  
Um nome de borda não pode ser repetido dentro de correspondência.  
Uma borda pode apontar em qualquer direção, mas deve ter uma direção explícita.  
OU e não os operadores não são suportados no padrão de correspondência. CORRESPONDÊNCIA pode ser combinada com outras expressões usando e na cláusula WHERE. No entanto, a combinação com outras expressões usando OR ou não, não é suportado. 

## <a name="examples"></a>Exemplos  
### <a name="a--find-a-friend"></a>A.  Localize um amigo 
 O exemplo a seguir cria uma tabela de nó e a tabela de borda de amigos, insere alguns dados e, em seguida, usa a correspondência localizar amigos de Alice, uma pessoa no gráfico.

 ```
 -- Create person node table
 CREATE TABLE dbo.Person (ID integer PRIMARY KEY, name varchar(50)) AS NODE;
 CREATE TABLE dbo.friend (start_date DATE) AS EDGE;

 -- Insert into node table
 INSERT INTO dbo.Person VALUES (1, 'Alice');
 INSERT INTO dbo.Person VALUES (2,'John');
 INSERT INTO dbo.Person VALUES (3, 'Jacob');

-- Insert into edge table
INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'Alice'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'John'), '9/15/2011');

INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'Alice'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'Jacob'), '10/15/2011');

INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'John'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'Jacob'), '10/15/2012');

-- use MATCH in SELECT to find friends of Alice
SELECT Person2.name AS FriendName
FROM Person Person1, friend, Person Person2
WHERE MATCH(Person1-(friend)->Person2)
AND Person1.name = 'Alice';

 ```

 ### <a name="b--find-friend-of-a-friend"></a>B.  Localizar friend de um amigo
 O exemplo a seguir tenta encontrar friend de um amigo de Alice. 

 ```
SELECT Person3.name AS FriendName 
FROM Person Person1, friend, Person Person2, friend friend2, Person Person3
WHERE MATCH(Person1-(friend)->Person2-(friend2)->Person3)
AND Person1.name = 'Alice';

 ```

### <a name="c--more-match-patterns"></a>C.  Mais `MATCH` padrões
 Estas são algumas maneiras de mais que um padrão pode ser especificado dentro de correspondência.

 ```
 -- Find a friend
    SELECT Person2.name AS FriendName
    FROM Person Person1, friend, Person Person2
    WHERE MATCH(Person1-(friend)->Person2);
    
-- The pattern can also be expressed as below

    SELECT Person2.name AS FriendName
    FROM Person Person1, friend, Person Person2 
    WHERE MATCH(Person2<-(friend)-Person1);


-- Find 2 people who are both friends with same person
    SELECT Person1.name AS Friend1, Person2.name AS Friend2
    FROM Person Person1, friend friend1, Person Person2, 
         friend friend2, Person Person0
    WHERE MATCH(Person1-(friend1)->Person0<-(friend2)-Person2);
    
-- this pattern can also be expressed as below

    SELECT Person1.name AS Friend1, Person2.name AS Friend2
    FROM Person Person1, friend friend1, Person Person2, 
         friend friend2, Person Person0
    WHERE MATCH(Person1-(friend1)->Person0 AND Person2-(friend2)->Person0);
 ```
 

## <a name="see-also"></a>Consulte também  
 [Criar tabela &#40; Gráfico SQL &#41;](../../t-sql/statements/create-table-sql-graph.md)   
 [INSERT (gráfico SQL)](../../t-sql/statements/insert-sql-graph.md)]  
 [Gráfico de processamento com o SQL Server 2017](../../relational-databases/graphs/sql-graph-overview.md)  

