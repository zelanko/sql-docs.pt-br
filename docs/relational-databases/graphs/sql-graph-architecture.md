---
title: Arquitetura do SQL Graph | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, architecture
ms.assetid: ''
author: shkale-msft
ms.author: shkale
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 79a85515322d492d4356d47f78da4b79489a223e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68811113"
---
# <a name="sql-graph-architecture"></a>Arquitetura do SQL Graph  
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Saiba como o SQL Graph é arquitetado. Conhecer os conceitos básicos tornará mais fácil entender outros artigos sobre o SQL Graph.
 
## <a name="sql-graph-database"></a>Banco de dados SQL Graph
Os usuários podem criar um grafo por banco de dados. Um grafo é uma coleção de tabelas de nó e borda. As tabelas de nó ou de borda podem ser criadas em qualquer esquema no banco de dados, mas todas pertencem a um grafo lógico. Uma tabela de nó é uma coleção de tipos semelhantes de nós. Por exemplo, uma tabela de nó Person contém todos os nós Person que pertencem a um grafo. Da mesma forma, uma tabela de borda é uma coleção de tipos de bordas semelhantes. Por exemplo, uma tabela de borda de amigos mantém todas as bordas que conectam uma pessoa a outra pessoa. Como os nós e as bordas são armazenados em tabelas, a maioria das operações com suporte em tabelas regulares tem suporte em tabelas de nó ou borda. 
 
 
![SQL-Graph-Architecture](../../relational-databases/graphs/media/sql-graph-architecture.png "Arquitetura do banco de dados SQL Graph")   

Figura 1: arquitetura de banco de dados do SQL Graph
 
## <a name="node-table"></a>Tabela de nó
Uma tabela de nó representa uma entidade em um esquema de grafo. Toda vez que uma tabela de nó é criada, juntamente com as colunas definidas pelo usuário, `$node_id` uma coluna implícita é criada, que identifica exclusivamente um determinado nó no banco de dados. Os valores em `$node_id` são gerados automaticamente e são uma combinação dessa `object_id` tabela de nó e um valor bigint gerado internamente. No entanto, `$node_id` quando a coluna é selecionada, um valor calculado na forma de uma cadeia de caracteres JSON é exibido. Além disso `$node_id` , é uma pseudo coluna, que mapeia para um nome interno com uma cadeia de caracteres hexadecimal. Quando você seleciona `$node_id` na tabela, o nome da coluna será exibido como `$node_id_<hex_string>`. Usar nomes de pseudo-colunas em consultas é a maneira recomendada de consultar a coluna `$node_id` interna e usar o nome interno com uma cadeia de caracteres hexadecimal deve ser evitada.

É recomendável que os usuários criem uma restrição exclusiva ou um `$node_id` índice na coluna no momento da criação da tabela de nó, mas se um não for criado, um índice não clusterizado padrão, exclusivo, será criado automaticamente. No entanto, qualquer índice em uma pseudo coluna gráfica é criado nas colunas internas subjacentes. Ou seja, um índice criado na `$node_id` coluna será exibido na coluna interna. `graph_id_<hex_string>`   


## <a name="edge-table"></a>Tabela de borda
Uma tabela de borda representa uma relação em um grafo. As bordas são sempre direcionadas e conectadas a dois nós. Uma tabela de borda permite que os usuários modelem relações muitos para muitos no grafo. Uma tabela de borda pode ou não ter nenhum atributo definido pelo usuário nela. Toda vez que uma tabela de borda é criada, juntamente com os atributos definidos pelo usuário, três colunas implícitas são criadas na tabela de borda:

|Nome da coluna    |Descrição  |
|---   |---  |
|`$edge_id`   |Identifica exclusivamente uma determinada borda no banco de dados. É uma coluna gerada e o valor é uma combinação de object_id da tabela de borda e um valor bigint gerado internamente. No entanto, `$edge_id` quando a coluna é selecionada, um valor calculado na forma de uma cadeia de caracteres JSON é exibido. `$edge_id`é uma pseudo coluna, que mapeia para um nome interno com cadeia de caracteres hexadecimal. Quando você seleciona `$edge_id` na tabela, o nome da coluna será exibido como `$edge_id_\<hex_string>`. Usar nomes de pseudo-colunas em consultas é a maneira recomendada de consultar a coluna `$edge_id` interna e usar o nome interno com uma cadeia de caracteres hexadecimal deve ser evitada. |
|`$from_id`   |Armazena o `$node_id` do nó, de onde a borda se origina.  |
|`$to_id`   |Armazena o `$node_id` do nó, no qual a borda é encerrada. |

Os nós aos quais uma determinada borda pode se conectar são regidos pelos dados inseridos `$from_id` nas `$to_id` colunas e. Na primeira versão, não é possível definir restrições na tabela de borda para impedir que ela se conecte a dois tipos de nós. Ou seja, uma borda pode conectar dois nós no grafo, independentemente de seus tipos.

De forma semelhante `$node_id` à coluna, é recomendável que os usuários criem um índice ou uma `$edge_id` restrição exclusiva na coluna no momento da criação da tabela de borda, mas se uma não for criada, um índice não clusterizado padrão será automaticamente criado nessa coluna. No entanto, qualquer índice em uma pseudo coluna gráfica é criado nas colunas internas subjacentes. Ou seja, um índice criado na `$edge_id` coluna será exibido na coluna interna. `graph_id_<hex_string>` Ele também é recomendado para cenários OLTP, que os usuários criam um índice nas colunas`$from_id`( `$to_id`,), para pesquisas mais rápidas na direção da borda.  

A Figura 2 mostra como as tabelas de nó e borda são armazenadas no banco de dados. 

![pessoa-amigos-tabelas](../../relational-databases/graphs/media/person-friends-tables.png "Nó Person e tabelas de borda de amigos")   

Figura 2: representação de tabela de nó e borda



## <a name="metadata"></a>Metadados
Use essas exibições de metadados para ver os atributos de uma tabela de nó ou borda.
 
### <a name="systables"></a>sys.tables
O novo tipo de bit a seguir, as colunas serão adicionadas a SYS. Tabelas. Se `is_node` é definido como 1, isso indica que a tabela é uma tabela de nó e `is_edge` se é definida como 1, que indica que a tabela é uma tabela de borda.
 
|Nome da coluna |Tipo de Dados |Descrição |
|--- |---|--- |
|is_node |bit |1 = Esta é uma tabela de nó |
|is_edge |bit |1 = Esta é uma tabela de borda |
 
### <a name="syscolumns"></a>sys.columns
A `sys.columns` exibição contém colunas `graph_type` adicionais e `graph_type_desc`, que indicam o tipo da coluna em tabelas de nó e borda.
 
|Nome da coluna |Tipo de Dados |Descrição |
|--- |---|--- |
|graph_type |INT |Coluna interna com um conjunto de valores. Os valores estão entre 1-8 para colunas de grafo e nulos para outros.  |
|graph_type_desc |nvarchar(60)  |coluna interna com um conjunto de valores |
 
A tabela a seguir lista os valores válidos `graph_type` para a coluna

|Valor da coluna  |Descrição  |
|---   |---   |
|1  |GRAPH_ID  |
|2  |GRAPH_ID_COMPUTED  |
|3  |GRAPH_FROM_ID  |
|4  |GRAPH_FROM_OBJ_ID  |
|5  |GRAPH_FROM_ID_COMPUTED  |
|6  |GRAPH_TO_ID  |
|7  |GRAPH_TO_OBJ_ID  |
|8  |GRAPH_TO_ID_COMPUTED  |


`sys.columns`também armazena informações sobre colunas implícitas criadas em tabelas de nó ou borda. As informações a seguir podem ser recuperadas de sys. Columns, no entanto, os usuários não podem selecionar essas colunas em uma tabela de nó ou borda. 

Colunas implícitas em uma tabela de nó

|Nome da coluna    |Tipo de Dados  |is_hidden  |Comentário  |
|---  |---|---|---  |
|graph_id_\<hex_string> |bigint |1  |coluna `graph_id` interna  |
|$node _id_\<hex_string> |NVARCHAR   |0  |Coluna de `node_id` nó externo  |

Colunas implícitas em uma tabela de borda

|Nome da coluna    |Tipo de Dados  |is_hidden  |Comentário  |
|---  |---|---|---  |
|graph_id_\<hex_string> |bigint |1  |coluna `graph_id` interna  |
|$edge _id_\<hex_string> |NVARCHAR   |0  |coluna `edge_id` externa  |
|from_obj_id_\<hex_string>  |INT    |1  |interno do nó`object_id`  |
|from_id_\<hex_string>  |bigint |1  |Interno do nó`graph_id`  |
|$from _id_\<hex_string> |NVARCHAR   |0  |externo do nó`node_id`  |
|to_obj_id_\<hex_string>    |INT    |1  |interno ao nó`object_id`  |
|to_id_\<hex_string>    |bigint |1  |Interno ao nó`graph_id`  |
|$to _id_\<hex_string>   |NVARCHAR   |0  |externo ao nó`node_id`  |
 
### <a name="system-functions"></a>Funções de sistema
As funções internas a seguir são adicionadas. Eles ajudarão os usuários a extrair informações das colunas geradas. Observe que, esses métodos não validarão a entrada do usuário. Se o usuário especificar um método `sys.node_id` inválido, ele extrairá a parte apropriada e a retornará. Por exemplo, OBJECT_ID_FROM_NODE_ID utilizará `$node_id` como entrada e retornará o object_id da tabela ao qual este nó pertence. 
 
|Interno   |Descrição  |
|---  |---  |
|OBJECT_ID_FROM_NODE_ID |Extrair o object_id de um`node_id`  |
|GRAPH_ID_FROM_NODE_ID  |Extrair o graph_id de um`node_id`  |
|NODE_ID_FROM_PARTS |Construir um node_id de um `object_id` e um`graph_id`  |
|OBJECT_ID_FROM_EDGE_ID |Extrair `object_id` de`edge_id`  |
|GRAPH_ID_FROM_EDGE_ID  |Extrair identidade de`edge_id`  |
|EDGE_ID_FROM_PARTS |Construir `edge_id` de `object_id` e identidade  |



## <a name="transact-sql-reference"></a>Referência do Transact-SQL 
Conheça as [!INCLUDE[tsql-md](../../includes/tsql-md.md)] extensões introduzidas no SQL Server e no banco de dados SQL do Azure, que permitem criar e consultar objetos de grafo. As extensões de linguagem de consulta ajudam a consultar e percorrer o grafo usando a sintaxe de arte ASCII.
 
### <a name="data-definition-language-ddl-statements"></a>Instruções de DDL (Linguagem de Definição de Dados)

|Tarefa   |Artigo relacionado  |Observações
|---  |---  |---  |
|CREATE TABLE |[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-sql-graph.md)|`CREATE TABLE`Agora é estendido para dar suporte à criação de uma tabela como nó ou como borda. Observe que uma tabela de borda pode ou não ter nenhum atributo definido pelo usuário.  |
|ALTER TABLE    |[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)|As tabelas de nó e borda podem ser alteradas da mesma maneira que uma tabela relacional `ALTER TABLE`, usando o. Os usuários podem adicionar ou modificar colunas, índices ou restrições definidas pelo usuário. No entanto, alterar as colunas internas do `$node_id` grafo `$edge_id`, como ou, resultará em um erro.  |
|CREATE INDEX   |[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  |Os usuários podem criar índices em pseudovariáveis e colunas definidas pelo usuário em tabelas de nó e borda. Todos os tipos de índice têm suporte, incluindo índices columnstore clusterizados e não clusterizados.  |
|CRIAR RESTRIÇÕES DE BORDA    |[RESTRIÇÕES de borda &#40;&#41;Transact-SQL](../../relational-databases/tables/graph-edge-constraints.md)  |Agora, os usuários podem criar restrições de borda em tabelas de borda para impor semântica específica e também manter a integridade dos dados  |
|DROP TABLE |[DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)  |As tabelas de nó e borda podem ser descartadas da mesma maneira que uma tabela relacional, usando o `DROP TABLE`. No entanto, nesta versão, não há restrições para garantir que nenhuma borda aponte para um nó excluído e a exclusão em cascata de bordas, após a exclusão de uma tabela de nó ou nó, não seja suportada. É recomendável que, se uma tabela de nó for descartada, os usuários descartarão todas as bordas conectadas aos nós nessa tabela de nó manualmente para manter a integridade do grafo.  |


### <a name="data-manipulation-language-dml-statements"></a>Instruções de DML (Linguagem de Manipulação de Dados)

|Tarefa   |Artigo relacionado  |Observações
|---  |---  |---  |
|INSERT |[INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-sql-graph.md)|A inserção em uma tabela de nó não é diferente de inserir em uma tabela relacional. Os valores da `$node_id` coluna são gerados automaticamente. A tentativa de inserir um valor `$node_id` na `$edge_id` coluna ou resultará em um erro. Os usuários devem fornecer valores `$from_id` para `$to_id` as colunas e ao inserir em uma tabela de borda. `$from_id`e `$to_id` são os `$node_id` valores dos nós que uma determinada borda conecta.  |
|Delete (excluir) | [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)|Os dados de tabelas de nó ou borda podem ser excluídos da mesma maneira que são excluídos das tabelas relacionais. No entanto, nesta versão, não há restrições para garantir que nenhuma borda aponte para um nó excluído e a exclusão em cascata de bordas, após a exclusão de um nó, não seja suportada. É recomendável que sempre que um nó for excluído, todas as bordas de conexão para esse nó também sejam excluídas, a fim de manter a integridade do grafo.  |
|UPDATE |[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  |Os valores em colunas definidas pelo usuário podem ser atualizados usando a instrução UPDATE. Não é permitido atualizar as colunas `$node_id`internas `$edge_id`do `$from_id` grafo `$to_id` ,, e.  |
|MESCLAR |[MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)  |`MERGE`Há suporte para a instrução em uma tabela de nó ou borda.  |


### <a name="query-statements"></a>Instruções de consulta

|Tarefa   |Artigo relacionado  |Observações
|---  |---  |---  |
|SELECT |[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)|Nós e bordas são armazenados como tabelas internamente, portanto, a maioria das operações com suporte em uma tabela no SQL Server ou no banco de dados SQL do Azure tem suporte nas tabelas de nó e borda  |
|MATCH  | [CORRESPONDER &#40;&#41;Transact-SQL](../../t-sql/queries/match-sql-graph.md)|A correspondência interna é introduzida para dar suporte à correspondência de padrões e passagem por meio do grafo.  |



## <a name="limitations-and-known-issues"></a>Limitações e problemas conhecidos  
Há certas limitações nas tabelas de nó e borda nesta versão:
* As tabelas temporárias locais ou globais não podem ser tabelas de nó ou de borda.
* Tipos de tabela e variáveis de tabela não podem ser declarados como uma tabela de nó ou borda. 
* As tabelas de nó e borda não podem ser criadas como tabelas temporais com controle de versão do sistema.   
* As tabelas de nó e borda não podem ter tabelas com otimização de memória.  
* Os usuários não podem `$from_id` atualizar `$to_id` as colunas e de uma borda usando a instrução UPDATE. Para atualizar os nós que uma borda conecta, os usuários precisarão inserir a nova borda apontando para novos nós e excluir o anterior.
* Não há suporte para consultas entre bancos de dados em objetos de grafo. 


## <a name="next-steps"></a>Próximas etapas
Para começar a usar a nova sintaxe, consulte [banco de dados SQL Graph-exemplo](./sql-graph-sample.md)
 

