---
title: Arquitetura do Graph SQL | Microsoft Docs
ms.custom: ''
ms.date: 04/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: graphs
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, architecture
ms.assetid: ''
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: 7cfba1fc79e44bb28a433c3b31fe5f4236037d6e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-graph-architecture"></a>Arquitetura do gráfico do SQL  
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Saiba como o SQL Graph foi projetado. Conhecer os conceitos básicos tornará mais fácil de entender outros artigos de SQL Graph.
 
## <a name="sql-graph-database"></a>Banco de dados SQL Graph
Os usuários podem criar um gráfico por banco de dados. Um gráfico é uma coleção de tabelas de nó e borda. Tabelas de borda ou nó podem ser criadas em qualquer esquema no banco de dados, mas pertencerem a um gráfico lógico. Uma tabela de nó é a coleção de tipo semelhante de nós. Por exemplo, uma tabela de nó da pessoa que contém todos os nós da pessoa que pertencem a um gráfico. Da mesma forma, uma tabela de borda é uma coleção de tipo semelhante de bordas. Por exemplo, uma tabela de borda de amigos contém todas as bordas que se conectam a uma pessoa para outra pessoa. Nós e bordas são armazenadas em tabelas, a maioria das operações com suporte em tabelas regulares é suportada em tabelas de nó ou borda. 
 
 
![arquitetura do gráfico de SQL](../../relational-databases/graphs/media/sql-graph-architecture.png "arquitetura de banco de dados do SQL Graph")   

Figura 1: arquitetura de banco de dados do SQL Graph
 
## <a name="node-table"></a>Tabela do nó
Uma tabela de nó representa uma entidade em um esquema de gráfico. Sempre que um nó criar tabela, juntamente com as colunas definidas pelo usuário, implícita `$node_id` coluna é criada, que identifica exclusivamente um nó específico no banco de dados. Os valores em `$node_id` são gerados automaticamente e são uma combinação de `object_id` de tabela nó e um valor gerado internamente bigint. No entanto, quando o `$node_id` coluna for selecionada, um valor calculado na forma de uma cadeia de caracteres JSON é exibido. Além disso, `$node_id` é uma pseudocoluna, que é mapeado para um nome interno com a cadeia de caracteres hexadecimal nele. Quando você seleciona `$node_id` da tabela, o nome da coluna será exibido como `$node_id_<hex_string>`. Usando nomes de colunas pseudo em consultas é a maneira recomendada de consulta interna `$node_id` coluna e usando o nome interno com a cadeia de caracteres hexadecimal devem ser evitados.

É recomendável que os usuários criam uma restrição exclusiva ou índice no `$node_id` coluna no momento da criação da tabela de nó, mas se um não for criada, um padrão de índice não clusterizado exclusivo é criado automaticamente. No entanto, qualquer índice em uma coluna de pseudo gráfico é criado em colunas subjacentes internas. Ou seja, um índice criado o `$node_id` coluna, serão exibidos na interno `graph_id_<hex_string>` coluna.   


## <a name="edge-table"></a>Tabela de borda
Uma tabela de borda representa uma relação em um gráfico. As bordas são sempre direcionadas e conecte-se dois nós. Uma tabela de borda permite aos usuários modelo relações de muitos-para-muitos no gráfico. Uma tabela de borda pode ou não ter nenhum atributo definido pelo usuário nele. Toda vez que uma tabela de borda é criada, junto com os atributos definidos pelo usuário, três colunas implícitas são criadas na tabela de borda:

|Nome da coluna    |Description  |
|---   |---  |
|`$edge_id`   |Identifica exclusivamente uma borda fornecida no banco de dados. É uma coluna gerada e o valor é uma combinação de object_id da tabela de borda e um valor gerado internamente bigint. No entanto, quando o `$edge_id` coluna for selecionada, um valor calculado na forma de uma cadeia de caracteres JSON é exibido. `$edge_id` é uma coluna pseudo, que é mapeado para um nome interno com a cadeia de caracteres hexadecimal nele. Quando você seleciona `$edge_id` da tabela, o nome da coluna será exibido como `$edge_id_\<hex_string>`. Usando nomes de colunas pseudo em consultas é a maneira recomendada de consulta interna `$edge_id` coluna e usando o nome interno com a cadeia de caracteres hexadecimal devem ser evitados. |
|`$from_id`   |Armazena o `$node_id` do nó, de onde se origina a borda.  |
|`$to_id`   |Armazena o `$node_id` do nó, em que a borda termina. |

Os nós que pode se conectar a uma determinado borda é controlado pelos dados inseridos no `$from_id` e `$to_id` colunas. Na primeira versão, não é possível definir restrições na tabela de borda para restringi-lo de se conectar a qualquer tipo de dois nós. Ou seja, uma borda pode se conectar a dois nós no gráfico, independentemente de seus tipos.

Semelhante do `$node_id` coluna, é recomendável que os usuários criar um índice exclusivo ou restrição a `$edge_id` coluna no momento da criação da tabela de borda, mas se um não for criada, um padrão de índice não clusterizado exclusivo é criado automaticamente no Essa coluna. No entanto, qualquer índice em uma coluna de pseudo gráfico é criado em colunas subjacentes internas. Ou seja, um índice criado o `$edge_id` coluna, serão exibidos na interno `graph_id_<hex_string>` coluna. Também é recomendável, para cenários OLTP, que os usuários a criar um índice em (`$from_id`, `$to_id`) colunas, para pesquisas mais rápidas na direção da borda.  

A Figura 2 mostra como as tabelas de nó e borda são armazenadas no banco de dados. 

![tabelas de amigos pessoa](../../relational-databases/graphs/media/person-friends-tables.png "tabelas de borda do nó de pessoa e amigos")   

Figura 2: Representação de tabela de borda e de nó



## <a name="metadata"></a>Metadados
Use essas exibições de metadados para ver os atributos de uma tabela de borda ou nó.
 
### <a name="systables"></a>sys.tables
O seguinte novo tipo de bit, colunas serão adicionadas para SYS. TABELAS. Se `is_node` é definido como 1, o que indica que a tabela é uma tabela de nó e se `is_edge` é definido como 1, o que indica que a tabela é uma tabela de borda.
 
|Nome da coluna |Tipo de dados |Description |
|--- |---|--- |
|is_node |bit |1 = essa é uma tabela de nó |
|is_edge |bit |1 = Este é uma tabela de borda |
 
### <a name="syscolumns"></a>sys.columns
O `sys.columns` exibição contém colunas adicionais `graph_type` e `graph_type_desc`, que indicam o tipo de coluna nas tabelas de nó e borda.
 
|Nome da coluna |Tipo de dados |Description |
|--- |---|--- |
|graph_type |int |Coluna interna com um conjunto de valores. Os valores estão entre 1-8 para colunas do gráfico e NULL para outras pessoas.  |
|graph_type_desc |nvarchar(60)  |coluna interna com um conjunto de valores |
 
A tabela a seguir lista os valores válidos para `graph_type` coluna

|Valor da coluna  |Description  |
|---   |---   |
|1  |GRAPH_ID  |
|2  |GRAPH_ID_COMPUTED  |
|3  |GRAPH_FROM_ID  |
|4  |GRAPH_FROM_OBJ_ID  |
|5  |GRAPH_FROM_ID_COMPUTED  |
|6  |GRAPH_TO_ID  |
|7  |GRAPH_TO_OBJ_ID  |
|8  |GRAPH_TO_ID_COMPUTED  |


`sys.columns` também armazena informações sobre as colunas implícitas criadas em tabelas de borda ou nó. Informações a seguir pode ser recuperada de Columns, no entanto, os usuários não é possível selecionar essas colunas de uma tabela de borda ou nó. 

Colunas implícitas em uma tabela de nó  
|Nome da coluna    |Tipo de Dados  |is_hidden  |Comentário  |
|---  |---|---|---  |
|graph_id_\<hex_string > |bigint |1  |coluna graph_id interno  |
|$node_id_\<hex_string > |NVARCHAR   |0  |Coluna de id do nó externo  |

Colunas implícitas em uma tabela de borda  
|Nome da coluna    |Tipo de Dados  |is_hidden  |Comentário  |
|---  |---|---|---  |
|graph_id_\<hex_string > |bigint |1  |coluna graph_id interno  |
|$edge_id_\<hex_string > |NVARCHAR   |0  |coluna de id da borda externa  |
|from_obj_id_\<hex_string>  |INT    |1  |interno da id de objeto de nó  |
|from_id_\<hex_string >  |bigint |1  |Internos do nó graph_id  |
|$from_id_\<hex_string > |NVARCHAR   |0  |externa da id de nó  |
|to_obj_id_\<hex_string>    |INT    |1  |a id de objeto de nó interno  |
|to_id_\<hex_string>    |bigint |1  |Nó graph_id interno  |
|$to_id_\<hex_string >   |NVARCHAR   |0  |externos ao id do nó  |
 
### <a name="system-functions"></a>Funções de sistema
As seguintes funções internas são adicionadas. Eles ajudarão os usuários extrair informações de colunas geradas. Observe que, esses métodos não validará a entrada do usuário. Se o usuário Especifica um inválido `sys.node_id` o método extrairá parte apropriada e retorná-la. Por exemplo, OBJECT_ID_FROM_NODE_ID terão um `$node_id` como entrada e retorna o object_id da tabela, este nó pertence. 
 
|Interno   |Description  |
|---  |---  |
|OBJECT_ID_FROM_NODE_ID |Extrair o object_id de um node_id  |
|GRAPH_ID_FROM_NODE_ID  |Extrair o graph_id de um node_id  |
|NODE_ID_FROM_PARTS |Construir um node_id de um object_id e um graph_id  |
|OBJECT_ID_FROM_EDGE_ID |Extrair object_id edge_id  |
|GRAPH_ID_FROM_EDGE_ID  |Extrair identidade edge_id  |
|EDGE_ID_FROM_PARTS |Construir edge_id object_id e identidade  |



## <a name="transact-sql-reference"></a>Referência do Transact-SQL 
Aprenda a [!INCLUDE[tsql-md](../../includes/tsql-md.md)] extensões introduzidas no SQL Server e banco de dados do SQL Azure, que permitem criar e consultar objetos de gráfico. As extensões de linguagem de consulta ajuda a consulta e percorrer o gráfico usando a sintaxe de arte ASCII.
 
### <a name="data-definition-language-ddl-statements"></a>Instruções de Definition Language (DDL) de dados
|Tarefa   |Tópico relacionado  |Observações
|---  |---  |---  |
|CREATE TABLE |[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-sql-graph.md)|`CREATE TABLE ` Agora é estendida para dar suporte à criação de uma tabela como nó ou como borda. Observe que uma tabela de borda pode ou pode não ter qualquer atributos definidos pelo usuário.  |
|ALTER TABLE    |[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)|Tabelas de nó e de borda podem ser alteradas da mesma forma que uma tabela relacional, usando o `ALTER TABLE`. Os usuários podem adicionar ou modificar colunas definidas pelo usuário, índices ou restrições. No entanto, como a alteração de colunas do gráfico interno, `$node_id` ou `$edge_id`, resultará em erro.  |
|CREATE INDEX   |[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  |Os usuários podem criar índices em colunas pseudo e colunas definidas pelo usuário nas tabelas de nó e borda. Todos os tipos de índice têm suporte, incluindo índices columnstore clusterizados e não clusterizados.  |
|DROP TABLE |[DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)  |Tabelas de nó e de borda podem ser descartadas da mesma forma que uma tabela relacional, usando o `DROP TABLE`. No entanto, nesta versão, não há restrições para garantir que não há bordas apontam para um nó excluído e não há suporte para a exclusão em cascata de bordas, após a exclusão de um nó ou uma tabela de nó. É recomendável que, se um nó de tabela for descartado, usuários descartar qualquer Bordas conectadas a nós nessa tabela nó manualmente para manter a integridade do gráfico.  |


### <a name="data-manipulation-language-dml-statements"></a>Instruções do Data Manipulation Language (DML)
|Tarefa   |Tópico relacionado  |Observações
|---  |---  |---  |
|INSERT |[INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-sql-graph.md)|Inserindo em uma tabela de nó não é diferente de inserção em uma tabela relacional. Os valores para `$node_id` coluna é gerada automaticamente. Tentativa de inserir um valor em `$node_id` ou `$edge_id` coluna resultará em erro. Os usuários devem fornecer valores para `$from_id` e `$to_id` colunas ao inserir em uma tabela de borda. `$from_id` e `$to_id` são o `$node_id` valores de nós que um determinado borda conecta.  |
|DELETE | [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)|Dados de tabelas de borda ou nó podem ser excluídos na mesma forma como ele é excluído do tabelas relacionais. No entanto, nesta versão, não há restrições para garantir que não há bordas apontam para um nó excluído e não há suporte para a exclusão em cascata de bordas, após a exclusão de um nó. Recomenda-se que sempre que um nó é excluído, todas as bordas de conexão para esse nó também são excluídas, para manter a integridade do gráfico.  |
|UPDATE |[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  |Valores em colunas definidas pelo usuário podem ser atualizados usando a instrução UPDATE. Atualizar as colunas do gráfico interno, `$node_id`, `$edge_id`, `$from_id` e `$to_id` não é permitido.  |
|MERGE |[MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)  |`MERGE` Não há suporte para a instrução em uma tabela de borda ou nó.  |


### <a name="query-statements"></a>Instruções de consulta
|Tarefa   |Tópico relacionado  |Observações
|---  |---  |---  |
|SELECT |[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)|Nós e bordas são armazenadas como tabelas internamente, portanto, a maioria das operações de suporte em uma tabela no SQL Server ou banco de dados do SQL Azure têm suporte nas tabelas de nó e borda  |
|MATCH  | [MATCH &#40;Transact-SQL&#41;](../../t-sql/queries/match-sql-graph.md)|CORRESPONDÊNCIA interna é apresentada para dar suporte a correspondência de padrões e passagem por meio de graph.  |



## <a name="limitations-and-known-issues"></a>Limitações e problemas conhecidos  
Há algumas limitações em tabelas de nó e borda nesta versão:
* Tabelas temporárias locais ou globais não podem ser tabelas de nó ou borda.
* Tipos de tabela e variáveis de tabela não podem ser declaradas como uma tabela de borda ou nó. 
* Não não possível criar tabelas de nó e de borda como tabelas temporais com versão do sistema.   
* Tabelas de borda e de nó não podem ser tabelas com otimização de memória.  
* Os usuários não é possível atualizar as from_id $ e $to_id colunas de uma borda usando a instrução UPDATE. Para atualizar os nós que uma borda conecta, os usuários terão a inserir a nova borda apontando para novos nós e excluir anterior.
* Não há suporte para as consultas em objetos de gráfico banco de dados. 


## <a name="next-steps"></a>Próximas etapas
Para começar a usar a nova sintaxe, consulte [Banco de dados SQL Graph – Exemplo](./sql-graph-sample.md)
 

