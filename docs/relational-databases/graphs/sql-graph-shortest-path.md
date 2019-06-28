---
title: O caminho mais CURTO (SQL Graph) | Microsoft Docs
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
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ed931a8b1918961b69cc0600f94aff6e4d68b9e1
ms.sourcegitcommit: 0a4879dad09c6c42ad1ff717e4512cfea46820e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67413983"
---
# <a name="shortestpath-transact-sql"></a>SHORTEST_PATH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver2015-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  Especifica um critério de pesquisa para um gráfico, que é pesquisado recursivamente ou repetidamente. SHORTEST_PATH pode ser usado dentro de MATCH com as tabelas de nó e de borda do graph, na instrução SELECT. 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="shortest-path"></a>Caminho mais curto
A função SHORTEST_PATH permite que você encontrar:    
* Um caminho mais curto entre dois nós determinado/entidades
* Única fonte menor caminho (s).
* Caminho mais curto de vários nós de origem para vários nós de destino.

Ele usa um padrão de comprimento arbitrário, como entrada e retorna um caminho mais curto que existe entre dois nós. Essa função só pode ser usada dentro de MATCH. Ele aceita um padrão de comprimento arbitrário e localiza um caminho mais curto no gráfico, que corresponde a esse padrão. A função retorna apenas um caminho mais curto entre dois nós determinado. Se existe, dois ou mais caminhos mais curtos do mesmo comprimento entre qualquer par de nó (s) de origem e de destino, a função retornará apenas um caminho que foi encontrado primeiro durante a passagem. Observe que, um padrão de comprimento arbitrário só pode ser especificado dentro de uma função SHORTEST_PATH. 

Consulte a [correspondência (SQL Graph)](../../t-sql/queries/match-sql-graph.md) para obter a sintaxe. 

## <a name="for-path"></a>PARA O CAMINHO
PARA o caminho deve ser usado com qualquer nome de tabela de nó ou borda na cláusula FROM, que farão parte de um padrão de comprimento arbitrário. PARA o caminho informa ao mecanismo que a tabela de nó ou borda retornará uma coleção ordenada que representa a lista de nós ou bordas percorridas ao longo do caminho do nó inicial ao nó final. Os atributos dessas tabelas não podem ser projetados diretamente na cláusula SELECT. Para o projeto atributos dessas tabelas, funções de agregação do caminho do graph deve ser usado.  

## <a name="arbitrary-length-pattern"></a>Padrão de comprimento arbitrário
Esse padrão inclui os nós e bordas que devem ser atravessadas repetidamente até que o nó desejado seja atingido ou até que o número máximo de iterações, conforme especificado no padrão for atendida. Cada vez que a consulta é executada, o resultado da execução desse padrão será uma coleção ordenada de nós e bordas percorridas ao longo do caminho do nó inicial ao nó final. Este é um padrão de sintaxe de estilo de expressão regular e os quantificadores de padrão de dois a seguir têm suporte:

* **‘+’** : Repita o padrão de 1 ou mais vezes. Encerrar assim que encontra-se um caminho mais curto.
* **{1,n}** : Repita o padrão de 1 para ' n'horas. Encerrar assim que uma mais curta for encontrada.

## <a name="lastnode"></a>LAST_NODE
Função LAST_NODE() permite o encadeamento de dois padrões de passagem de comprimento arbitrário. Ele pode ser usado em cenários em que:    
* Mais de um padrões de caminho mais curto são usados em uma consulta e um padrão de começa no último nó do padrão anterior.
* Mesclagem dois padrões de caminho mais curtos em LAST_NODE() o mesmo.

## <a name="graph-path-order"></a>Ordem do caminho de gráfico
Ordem de caminho gráfico se refere a ordem dos dados no caminho de saída. A ordem de caminho de saída sempre inicia na parte do padrão seguido de nós/bordas que aparecem na parte recursiva de não-recursivo. A ordem na qual o gráfico é percorrido durante a execução da otimização de consulta não tem nada a ver com a ordem impressa na saída. Da mesma forma, a direção da seta no padrão de recursivo também não afeta a ordem de caminho do gráfico. 

## <a name="graph-path-aggregate-functions"></a>Funções de agregação de caminho do gráfico
Uma vez que os nós e bordas envolvidas no padrão de comprimento arbitrário retorno uma coleção (de nó (s) e edge(s) percorridas nesse caminho), os usuários não é possível projetar os atributos diretamente usando a sintaxe tablename.attributename convencional. Para consultas onde ela é necessária para valores de atributo de projeto intermediárias nó ou borda das tabelas de, no caminho percorrido, use as funções de agregação de caminho gráfico a seguir: STRING_AGG, LAST_VALUE, SUM, AVG, MIN, MAX e COUNT. A sintaxe geral para usar essas funções de agregação na cláusula SELECT é:

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

### <a name="stringagg"></a>STRING_AGG
A função STRING_AGG usa uma expressão e o separador como entrada e retorna uma cadeia de caracteres. Os usuários podem usar essa função na cláusula SELECT para atributos de projeto de nós intermediários ou bordas no caminho percorrido. 

### <a name="lastvalue"></a>LAST_VALUE
Para o projeto de atributos do último nó do caminho percorrido, função de agregação LAST_VALUE podem ser usados. É um erro para fornecer um alias de tabela de borda como uma entrada para essa função, somente os nomes de tabela do nó ou aliases podem ser usados.

**Último nó**: O último nó refere-se para o nó que é exibido por último no caminho percorrido, independentemente da direção da seta no predicado de correspondência. Por exemplo: `MATCH(SHORTEST_PATH(n(-(e)->p)+) )`. Aqui, o último nó no caminho será o último nó P visitado. 

Enquanto o último nó é o último nó enésimo no caminho de gráfico de saída para esse padrão: `MATCH(SHORTEST_PATH((n<-(e)-)+p))`    

### <a name="sum"></a>SUM
Essa função retorna a soma dos valores de atributo de nó/borda fornecida ou uma expressão que apareceu no caminho percorrido.

### <a name="count"></a>COUNT
Essa função retorna o número de valores não nulos do atributo de nó/borda desejado no caminho. A função COUNT dá suporte a ' *' operador com um alias de tabela de nó ou borda. Sem o alias de tabela nó ou borda, o uso de * é ambíguo e resultará em um erro.

    {  COUNT( <expression> | <node_or_edge_alias>.* )  <order_clause>  }


### <a name="avg"></a>AVG
Retorna a média dos valores de atributo de nó/borda fornecida ou uma expressão que apareceu no caminho percorrido.

### <a name="min"></a>MIN
Retorna o valor mínimo dos valores de atributo de nó/borda fornecida ou uma expressão que apareceu no caminho percorrido.

### <a name="max"></a>MAX
Retorna o valor máximo dos valores de atributo de nó/borda fornecida ou uma expressão que apareceu no caminho percorrido.

## <a name="remarks"></a>Comentários  
função de shortest_path só pode ser usada dentro de MATCH.     
Somente há suporte para LAST_NODE dentro de shortest_path.     
Não há suporte para a localização ponderada de caminho mais curto, todos os caminhos ou todos os caminhos mais curtos.         
Em alguns casos, os planos ruins podem ser gerados para consultas com maior número de saltos, o que resulta em maior tempo de execução de consulta. Usar uma dica de junção de hash pode ajudar.    


## <a name="examples"></a>Exemplos 
Para as consultas de exemplo mostradas aqui, vamos ot usam o nó e tabelas de borda criados no [exemplo SQL Graph](./sql-graph-sample.md)

### <a name="a--find-shortest-path-between-2-people"></a>A.  Localizar o caminho mais curto entre 2 pessoas
 No exemplo a seguir, podemos encontrar o caminho mais curto entre Jacob e Alice. Precisaremos o nó de pessoa e a borda FriendOf criado a partir do script de exemplo do gráfico. 

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

 ### <a name="b--find-shortest-path-from-a-given-node-to-all-other-nodes-in-the-graph"></a>B.  Localize o caminho mais curto de um determinado nó para todos os outros nós no gráfico. 
 O exemplo a seguir localiza todas as pessoas que Jacob está conectado no gráfico e o caminho mais curto, começando por Jacob todas essas pessoas. 

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

### <a name="c--count-the-number-of-hopslevels-traversed-to-go-from-one-person-to-another-in-the-graph"></a>C.  Conte o número de saltos/níveis atravessada para ir de uma pessoa para outra no gráfico.
 O exemplo a seguir localiza o caminho mais curto entre Jacob e Alice e imprime o número de saltos que leva para passar de Jacob para Alice. 

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

### <a name="d-find-people-1-3-hops-away-from-a-given-person"></a>D. Localizar pessoas saltos de 1 a 3 para fora de uma determinada pessoa
O exemplo a seguir localiza o caminho mais curto entre Jacob e todas as pessoas que ele está conectado em saltos de 1 a 3 do grafo longe em contato com ele. 

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

### <a name="e-find-people-exactly-2-hops-away-from-a-given-person"></a>E. Localizar pessoas exatamente 2 saltos para fora de uma determinada pessoa
O exemplo a seguir localiza o caminho mais curto entre Jacob e pessoas que estão exatamente 2 saltos em contato com ele no gráfico. 

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
 [CORRESPONDÊNCIA (SQL Graph)](../../t-sql/queries/match-sql-graph.md)    
 [CREATE TABLE &#40;SQL Graph&#41;](../../t-sql/statements/create-table-sql-graph.md)   
 [INSERT (SQL Graph)](../../t-sql/statements/insert-sql-graph.md)]  
 [Processamento de grafo com o SQL Server 2017](../../relational-databases/graphs/sql-graph-overview.md)     
 
