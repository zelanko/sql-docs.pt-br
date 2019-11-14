---
title: CAMINHO mais curto (SQL Graph) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
f1_keywords:
- SHORTEST PATH
- SHORTEST_PATH
dev_langs:
- TSQL
helpviewer_keywords:
- MATCH statement [SQL Server], SQL graph
- SQL graph, MATCH statement
author: shkale-msft
ms.author: shkale
monikerRange: =azuresqldb-current||>=sql-server-ver15||=sqlallproducts-allversions||=azuresqldb-mi-current
ms.openlocfilehash: 9318a34b4853937983b107491c9210de80e5506c
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056397"
---
# <a name="shortest_path-transact-sql"></a>SHORTEST_PATH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver2015-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  Especifica um critério de pesquisa para um grafo, que é pesquisado recursiva ou repetidamente. SHORTEST_PATH pode ser usada dentro da correspondência com tabelas de borda e nó do grafo, na instrução SELECT. 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="shortest-path"></a>Caminho mais curto
A função SHORTEST_PATH permite que você encontre:    
* Um caminho mais curto entre dois nós/entidades determinados
* Caminho (s) de fonte única mais curta.
* Caminho mais curto de vários nós de origem para vários nós de destino.

Ele usa um padrão de comprimento arbitrário como entrada e retorna um caminho mais curto que existe entre dois nós. Essa função só pode ser usada dentro de MATCH. A função retorna apenas um caminho mais curto entre dois nós determinados. Se houver, dois ou mais caminhos mais curtos com o mesmo comprimento entre qualquer par de nó (s) de origem e de destino, a função retornará apenas um caminho que foi encontrado primeiro durante a passagem. Observe que, um padrão de comprimento arbitrário só pode ser especificado dentro de uma função SHORTEST_PATH. 

Consulte a [correspondência (SQL Graph)](../../t-sql/queries/match-sql-graph.md) para obter a sintaxe. 

## <a name="for-path"></a>PARA O CAMINHO
FOR PATH deve ser usado com qualquer nome de tabela de nó ou borda na cláusula FROM, que participará de um padrão de comprimento arbitrário. FOR PATH informa ao mecanismo que a tabela de nó ou borda retornará uma coleção ordenada que representa a lista de nós ou bordas encontradas ao longo do caminho atravessado. Os atributos dessas tabelas não podem ser projetados diretamente na cláusula SELECT. Para atributos de projeto dessas tabelas, as funções de agregação de caminho do grafo devem ser usadas.  

## <a name="arbitrary-length-pattern"></a>Padrão de comprimento arbitrário
Esse padrão inclui os nós e as bordas que devem ser percorridas repetidamente até que o nó desejado seja atingido ou até que o número máximo de iterações, conforme especificado no padrão, seja atendido. Cada vez que a consulta é executada, o resultado da execução desse padrão será uma coleção ordenada de nós e bordas atravessados ao longo do caminho do nó inicial até o nó final. Este é um padrão de sintaxe de estilo de expressão regular e os dois quantificadores de padrão a seguir têm suporte:

* **' + '** : Repetir o padrão 1 ou mais vezes. É encerrado assim que encontra um caminho mais curto.
* **{1, n}** : repita o padrão 1 para ' n' vezes. Terminar assim que um mais curto for encontrado.

## <a name="last_node"></a>LAST_NODE
A função LAST_NODE () permite encadear dois padrões de passagem de comprimento arbitrário. Ele pode ser usado em cenários em que:    
* Mais de um caminho mais curto é usado em uma consulta e um padrão começa no último nó do padrão anterior.
* Dois padrões de caminho mais curtos mesclam no mesmo LAST_NODE ().

## <a name="graph-path-order"></a>Ordem do caminho do grafo
A ordem do caminho do grafo refere-se à ordem dos dados no caminho de saída. A ordem do caminho de saída sempre é iniciada na parte não recursiva do padrão seguido pelos nós/bordas que aparecem na parte recursiva. A ordem na qual o grafo é atravessado durante a otimização/execução da consulta não tem nada a ver com a ordem impressa na saída. Da mesma forma, a direção da seta no padrão recursivo também não afeta a ordem do caminho do grafo. 

## <a name="graph-path-aggregate-functions"></a>Funções de agregação de caminho do grafo
Como os nós e as bordas envolvidos no padrão de comprimento arbitrário retornam uma coleção (de nó (s) e borda (s) atravessados nesse caminho), os usuários não podem projetar os atributos diretamente usando a sintaxe convencional TableName. AttributeName. Para consultas em que é necessário projetar valores de atributo do nó intermediário ou tabelas de borda, no caminho atravessado, use as seguintes funções de agregação de caminho do grafo: STRING_AGG, LAST_VALUE, SUM, AVG, MIN, MAX e COUNT. A sintaxe geral para usar essas funções de agregação na cláusula SELECT é:

```
<GRAPH_PATH_AGGREGATE_FUNCTION>(<expression> , <separator>)  <order_clause>

    <order_clause> ::=
        { WITHIN GROUP (GRAPH PATH) }

    <GRAPH_PATH_AGGREGATE_FUNCTION> ::=
          STRING_AGG
        | LAST_VALUE
        | SUM
        | COUNT
        | AVG
        | MIN
        | MAX

```

### <a name="string_agg"></a>STRING_AGG
A função STRING_AGG usa uma expressão e um separador como entrada e retorna uma cadeia de caracteres. Os usuários podem usar essa função na cláusula SELECT para projetar atributos de nós intermediários ou bordas no caminho percorridos. 

### <a name="last_value"></a>LAST_VALUE
Para atributos de projeto do último nó do caminho percorrido, LAST_VALUE função de agregação pode ser usada. É um erro fornecer um alias de tabela de borda como uma entrada para essa função, somente nomes de tabela de nó ou aliases podem ser usados.

**Último nó**: o último nó refere-se ao nó que aparece por último no caminho atravessado, independentemente da direção da seta no predicado Match. Por exemplo: `MATCH(SHORTEST_PATH(n(-(e)->p)+) )`. Aqui, o último nó no caminho será o último nó P visitado. 

Enquanto que o último nó é o último nó enésimo no caminho do grafo de saída para esse padrão: `MATCH(SHORTEST_PATH((n<-(e)-)+p))`    

### <a name="sum"></a>SUM
Essa função retorna a soma dos valores de atributo de nó/borda fornecidos ou expressão que apareceu no caminho atravessado.

### <a name="count"></a>COUNT
Essa função retorna o número de valores não nulos do atributo de nó/borda desejado no caminho. A função COUNT dá suporte ao operador '\*' com um nó ou alias de tabela de borda. Sem o alias de tabela de nó ou borda, o uso de \* é ambíguo e resultará em um erro.

    {  COUNT( <expression> | <node_or_edge_alias>.* )  <order_clause>  }


### <a name="avg"></a>AVG
Retorna a média de valores de atributo de nó/borda fornecidos ou expressão que apareceu no caminho atravessado.

### <a name="min"></a>MIN
Retorna o valor mínimo dos valores de atributo de nó/borda fornecidos ou expressão que apareceu no caminho atravessado.

### <a name="max"></a>MAX
Retorna o valor máximo dos valores de atributo de nó/borda fornecidos ou expressão que apareceu no caminho atravessado.

## <a name="remarks"></a>Remarks  
shortest_path função só pode ser usada dentro de MATCH.     
Só há suporte para LAST_NODE no shortest_path.     
Encontrando um caminho mais curto ponderado, não há suporte para todos os caminhos ou todos os caminhos mais curtos.         
Em alguns casos, os planos inválidos podem ser gerados para consultas com um número maior de saltos, o que resulta em tempos de execução de consulta mais altos. O uso de uma dica de junção hash pode ajudar.    


## <a name="examples"></a>Exemplos 
Para as consultas de exemplo mostradas aqui, vamos usar as tabelas node e Edge criadas no [SQL Graph Sample](./sql-graph-sample.md)

### <a name="a--find-shortest-path-between-2-people"></a>A.  Localizar caminho mais curto entre 2 pessoas
 No exemplo a seguir, encontramos um caminho mais curto entre Jacob e Alice. Precisaremos do nó Person e da borda FriendOf criada a partir do script de exemplo do Graph. 

 ```
SELECT PersonName, Friends
FROM (  
    SELECT
        Person1.name AS PersonName, 
        STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends,
        LAST_VALUE(Person2.name) WITHIN GROUP (GRAPH PATH) AS LastNode
    FROM
        Person AS Person1,
        friendOf FOR PATH AS fo,
        Person FOR PATH  AS Person2
    WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2)+))
    AND Person1.name = 'Jacob'
) AS Q
WHERE Q.LastNode = 'Alice'
 ```

 ### <a name="b--find-shortest-path-from-a-given-node-to-all-other-nodes-in-the-graph"></a>b.  Localize o caminho mais curto de um determinado nó para todos os outros nós no grafo. 
 O exemplo a seguir localiza todas as pessoas às quais o Jacob está conectado no grafo e o caminho mais curto, começando de Jacob a todas essas pessoas. 

 ```
SELECT
    Person1.name AS PersonName, 
    STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends
FROM
    Person AS Person1,
    friendOf FOR PATH AS fo,
    Person FOR PATH  AS Person2
WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2)+))
AND Person1.name = 'Jacob'
 ```

### <a name="c--count-the-number-of-hopslevels-traversed-to-go-from-one-person-to-another-in-the-graph"></a>C.  Conte o número de saltos/níveis atravessados para passar de uma pessoa para outra no grafo.
 O exemplo a seguir localiza o caminho mais curto entre Jacob e Alice e imprime o número de saltos necessários para ir de Jacob para Alice. 

 ```
 SELECT PersonName, Friends, levels
FROM (  
    SELECT
        Person1.name AS PersonName, 
        STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends,
        LAST_VALUE(Person2.name) WITHIN GROUP (GRAPH PATH) AS LastNode,
        COUNT(Person2.name) WITHIN GROUP (GRAPH PATH) AS levels
    FROM
        Person AS Person1,
        friendOf FOR PATH AS fo,
        Person FOR PATH  AS Person2
    WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2)+))
    AND Person1.name = 'Jacob'
) AS Q
WHERE Q.LastNode = 'Alice'
 ```

### <a name="d-find-people-1-3-hops-away-from-a-given-person"></a>D. Localizar as pessoas 1-3 saltos de distância de uma determinada pessoa
O exemplo a seguir localiza o caminho mais curto entre Jacob e todas as pessoas às quais ele está conectado no grafo 1-3 saltos longe dele. 

```
SELECT
    Person1.name AS PersonName, 
    STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends
FROM
    Person AS Person1,
    friendOf FOR PATH AS fo,
    Person FOR PATH  AS Person2
WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2){1,3}))
AND Person1.name = 'Jacob'
```

### <a name="e-find-people-exactly-2-hops-away-from-a-given-person"></a>E. Localizar pessoas exatamente 2 saltos longe de uma determinada pessoa
O exemplo a seguir localiza o caminho mais curto entre Jacob e as pessoas que são exatamente 2 saltos de fora dele no grafo. 

```
SELECT PersonName, Friends
FROM (
    SELECT
        Person1.name AS PersonName, 
        STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends,
        COUNT(Person2.name) WITHIN GROUP (GRAPH PATH) AS levels
    FROM
        Person AS Person1,
        friendOf FOR PATH AS fo,
        Person FOR PATH  AS Person2
    WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2){1,3}))
    AND Person1.name = 'Jacob'
) Q
WHERE Q.levels = 2
```

## <a name="see-also"></a>Consulte também  
 [Match (SQL Graph)](../../t-sql/queries/match-sql-graph.md)    
 [CREATE TABLE &#40;SQL Graph&#41;](../../t-sql/statements/create-table-sql-graph.md)   
 [INSERT (SQL Graph)](../../t-sql/statements/insert-sql-graph.md)]  
 [Processamento de grafo com o SQL Server 2017](../../relational-databases/graphs/sql-graph-overview.md)     
 
