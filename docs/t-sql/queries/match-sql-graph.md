---
description: MATCH (Transact-SQL)
title: MATCH (SQL Graph) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- MATCH
- MATCH_TSQL
- SHORTEST_PATH
dev_langs:
- TSQL
helpviewer_keywords:
- MATCH statement [SQL Server], SQL graph
- SQL graph, MATCH statement
- Shortest Path, shortest_path
author: shkale-msft
ms.author: shkale
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8a98fd2557655672389f5372009f3cf0adaa3ba9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459135"
---
# <a name="match-transact-sql"></a>MATCH (Transact-SQL)
[!INCLUDE[SQL Server 2017](../../includes/applies-to-version/sqlserver2017.md)]

  Especifica um critério de pesquisa para um gráfico. MATCH pode ser usado apenas com tabelas de nó de gráfico e borda, na instrução SELECT como parte da cláusula WHERE. 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
MATCH (<graph_search_pattern>)

<graph_search_pattern>::=
  {  
      <simple_match_pattern> 
    | <arbitrary_length_match_pattern>  
    | <arbitrary_length_match_last_node_predicate> 
  }

<simple_match_pattern>::=
  {
      LAST_NODE(<node_alias>) | <node_alias>   { 
          { <-( <edge_alias> )- } 
        | { -( <edge_alias> )-> }
        <node_alias> | LAST_NODE(<node_alias>)
        } 
  }
  [ { AND } { ( <simple_match_pattern> ) } ]
  [ ,...n ]

<node_alias> ::=
  node_table_name | node_table_alias 

<edge_alias> ::=
  edge_table_name | edge_table_alias


<arbitrary_length_match_pattern>  ::=
  { 
    SHORTEST_PATH( 
      <arbitrary_length_pattern> 
      [ { AND } { <arbitrary_length_pattern> } ] 
      [ ,…n] 
    )
  } 

<arbitrary_length_match_last_node_predicate> ::=
  {  LAST_NODE( <node_alias> ) = LAST_NODE( <node_alias> ) }


<arbitrary_length_pattern> ::=
    {  LAST_NODE( <node_alias> )   | <node_alias>
     ( <edge_first_al_pattern> [<edge_first_al_pattern>…,n] )
     <al_pattern_quantifier> 
  }
    |  ( {<node_first_al_pattern> [<node_first_al_pattern> …,n] )
        <al_pattern_quantifier> 
        LAST_NODE( <node_alias> ) | <node_alias> 
 }
    
<edge_first_al_pattern> ::=
  { (  
        { -( <edge_alias> )->   } 
      | { <-( <edge_alias> )- } 
      <node_alias>
      ) 
  } 

<node_first_al_pattern> ::=
  { ( 
      <node_alias> 
        { <-( <edge_alias> )- } 
      | { -( <edge_alias> )-> }
      ) 
  } 


<al_pattern_quantifier> ::=
  {
        +
      | { 1 , n }
  }

n -  positive integer only.
 
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*graph_search_pattern*  
Especifica o padrão a ser pesquisado ou o caminho a ser percorrido no gráfico. Esse padrão usa a sintaxe de arte ASCII para percorrer um caminho no gráfico. O padrão varia de um nó para outro por meio de uma borda, na direção da seta fornecida. Os nomes de borda ou aliases são fornecidos em parênteses. Os nomes de nó ou os aliases são exibidos nas duas extremidades da seta. A seta pode apontar para qualquer direção no padrão.

*node_alias*  
Nome ou alias de uma tabela de nó fornecida na cláusula FROM.

*edge_alias*  
Nome ou alias de uma tabela de borda fornecida na cláusula FROM.

*SHORTEST_PATH*   
A função de caminho mais curta é usada para localizar o caminho mais curto entre dois nós ou entre um determinado nó e todos os outros nós em um gráfico. Ela usa como entrada um padrão de comprimento arbitrário que é pesquisado repetidamente em um gráfico. 

*arbitrary_length_match_pattern*  
Especifica os nós e bordas que precisam ser atravessadas repetidamente até atingir o nó desejado ou o número máximo de iterações, conforme especificado no padrão for atendido. 

*al_pattern_quantifier*   
O padrão de comprimento arbitrário considera quantificadores padrão de estilo de expressão regular para especificar o número de vezes que um padrão de pesquisa fornecido é repetido. Os quantificadores padrão de pesquisa compatíveis são:   
* **+** : Repete o padrão por 1 ou mais vezes. É encerrado assim que encontra um caminho mais curto.    
* **{1,n}** : repete o padrão 1 por “n” horas. É encerrado assim que encontra um caminho mais curto.     

## <a name="remarks"></a>Comentários  
Os nomes de nó dentro de MATCH podem ser repetidos.  Em outras palavras, um nó pode ser percorrido um número arbitrário de vezes na mesma consulta.  
Um nome de borda não pode ser repetido dentro de MATCH.  
Uma borda pode apontar para qualquer direção, mas deve ter uma direção explícita.  
Os operadores OR ou NOT não são compatíveis com o padrão MATCH. MATCH pode ser combinado com outras expressões usando AND na cláusula WHERE. No entanto, não há suporte para a combinação dele com outras expressões usando OR ou NOT. 

## <a name="examples"></a>Exemplos  
### <a name="a--find-a-friend"></a>a.  Encontrar um amigo 
 O exemplo a seguir cria uma tabela de nó Person e a tabela de Borda friends, insere alguns dados e, em seguida, usa MATCH para encontrar amigos de Alice, uma pessoa no gráfico.

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

 ### <a name="b--find-friend-of-a-friend"></a>B.  Encontrar um amigo de um amigo
 O exemplo a seguir tenta encontrar um amigo de um amigo de Alice. 

 ```
SELECT Person3.name AS FriendName 
FROM Person Person1, friend, Person Person2, friend friend2, Person Person3
WHERE MATCH(Person1-(friend)->Person2-(friend2)->Person3)
AND Person1.name = 'Alice';

 ```

### <a name="c--more-match-patterns"></a>C.  Mais padrões de `MATCH`
 Estas são algumas outras maneiras pelas quais um padrão pode ser especificado dentro de MATCH.

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
 

## <a name="see-also"></a>Consulte Também  
 [CREATE TABLE &#40;SQL Graph&#41;](../../t-sql/statements/create-table-sql-graph.md)   
 [INSERT (SQL Graph)](../../t-sql/statements/insert-sql-graph.md)]  
 [Processamento de grafo com o SQL Server 2017](../../relational-databases/graphs/sql-graph-overview.md)  
