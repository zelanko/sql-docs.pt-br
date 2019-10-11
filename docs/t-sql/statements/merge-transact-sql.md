---
title: MERGE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/20/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- MERGE
- MERGE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- updating data [SQL Server]
- modifying data [SQL Server], MERGE statement
- MERGE statement [SQL Server]
- adding data
- DML [SQL Server], MERGE statement
- table modifications [SQL Server], MERGE statement
- data manipulation language [SQL Server], MERGE statement
- inserting data
ms.assetid: c17996d6-56a6-482f-80d8-086a3423eecc
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0a49bef9dc75beea0e098908362f198b60a8b92c
ms.sourcegitcommit: 445842da7c7d216b94a9576e382164c67f54e19a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/30/2019
ms.locfileid: "71680830"
---
# <a name="merge-transact-sql"></a>MERGE (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Executa operações de inserção, atualização ou exclusão em uma tabela de destino usando os resultados de uma união com uma tabela de origem. Por exemplo, sincronize duas tabelas inserindo, atualizando ou excluindo linhas em uma tabela com base nas diferenças encontradas na outra tabela.  
  
**Dica de desempenho:** O comportamento condicional descrito para a instrução de MERGE funciona melhor quando as duas tabelas têm uma mistura complexa de características coincidentes. Por exemplo, inserindo uma linha se ela não existir ou atualizando uma linha se ela tiver correspondência. Ao simplesmente atualizar uma tabela com base nas linhas de outra tabela, melhore o desempenho e a escalabilidade com as instruções básicas INSERT, UPDATE e DELETE. Por exemplo:  
  
```sql
INSERT tbl_A (col, col2)  
SELECT col, col2
FROM tbl_B
WHERE NOT EXISTS (SELECT col FROM tbl_A A2 WHERE A2.col = tbl_B.col);  
```  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```
[ WITH <common_table_expression> [,...n] ]  
MERGE
    [ TOP ( expression ) [ PERCENT ] ]
    [ INTO ] <target_table> [ WITH ( <merge_hint> ) ] [ [ AS ] table_alias ]  
    USING <table_source>
    ON <merge_search_condition>  
    [ WHEN MATCHED [ AND <clause_search_condition> ]  
        THEN <merge_matched> ] [ ...n ]  
    [ WHEN NOT MATCHED [ BY TARGET ] [ AND <clause_search_condition> ]  
        THEN <merge_not_matched> ]  
    [ WHEN NOT MATCHED BY SOURCE [ AND <clause_search_condition> ]  
        THEN <merge_matched> ] [ ...n ]  
    [ <output_clause> ]  
    [ OPTION ( <query_hint> [ ,...n ] ) ]
;  
  
<target_table> ::=  
{
    [ database_name . schema_name . | schema_name . ]  
  target_table  
}  
  
<merge_hint>::=  
{  
    { [ <table_hint_limited> [ ,...n ] ]  
    [ [ , ] INDEX ( index_val [ ,...n ] ) ] }  
}  
  
<table_source> ::=
{  
    table_or_view_name [ [ AS ] table_alias ] [ <tablesample_clause> ]
        [ WITH ( table_hint [ [ , ]...n ] ) ]
  | rowset_function [ [ AS ] table_alias ]
        [ ( bulk_column_alias [ ,...n ] ) ]
  | user_defined_function [ [ AS ] table_alias ]  
  | OPENXML <openxml_clause>
  | derived_table [ AS ] table_alias [ ( column_alias [ ,...n ] ) ]
  | <joined_table>
  | <pivoted_table>
  | <unpivoted_table>
}  
  
<merge_search_condition> ::=  
    <search_condition>  
  
<merge_matched>::=  
    { UPDATE SET <set_clause> | DELETE }  
  
<set_clause>::=  
SET  
  { column_name = { expression | DEFAULT | NULL }  
  | { udt_column_name.{ { property_name = expression  
                        | field_name = expression }  
                        | method_name ( argument [ ,...n ] ) }  
    }  
  | column_name { .WRITE ( expression , @Offset , @Length ) }  
  | @variable = expression  
  | @variable = column = expression  
  | column_name { += | -= | *= | /= | %= | &= | ^= | |= } expression  
  | @variable { += | -= | *= | /= | %= | &= | ^= | |= } expression  
  | @variable = column { += | -= | *= | /= | %= | &= | ^= | |= } expression  
  } [ ,...n ]
  
<merge_not_matched>::=  
{  
    INSERT [ ( column_list ) ]
        { VALUES ( values_list )  
        | DEFAULT VALUES }  
}  
  
<clause_search_condition> ::=  
    <search_condition>  
  
<search condition> ::=  
    MATCH(<graph_search_pattern>) | <search_condition_without_match> | <search_condition> AND <search_condition>

<search_condition_without_match> ::=
    { [ NOT ] <predicate> | ( <search_condition_without_match> )
    [ { AND | OR } [ NOT ] { <predicate> | ( <search_condition_without_match> ) } ]
[ ,...n ]  

<predicate> ::=
    { expression { = | < > | ! = | > | > = | ! > | < | < = | ! < } expression
    | string_expression [ NOT ] LIKE string_expression
  [ ESCAPE 'escape_character' ]
    | expression [ NOT ] BETWEEN expression AND expression
    | expression IS [ NOT ] NULL
    | CONTAINS
  ( { column | * } , '< contains_search_condition >' )
    | FREETEXT ( { column | * } , 'freetext_string' )
    | expression [ NOT ] IN ( subquery | expression [ ,...n ] )
    | expression { = | < > | ! = | > | > = | ! > | < | < = | ! < }
  { ALL | SOME | ANY} ( subquery )
    | EXISTS ( subquery ) }

<graph_search_pattern> ::=
    { <node_alias> {
                      { <-( <edge_alias> )- }
                    | { -( <edge_alias> )-> }
                    <node_alias>
                   }
    }
  
<node_alias> ::=
    node_table_name | node_table_alias

<edge_alias> ::=
    edge_table_name | edge_table_alias

<output_clause>::=  
{  
    [ OUTPUT <dml_select_list> INTO { @table_variable | output_table }  
        [ (column_list) ] ]  
    [ OUTPUT <dml_select_list> ]  
}  
  
<dml_select_list>::=  
    { <column_name> | scalar_expression }
        [ [AS] column_alias_identifier ] [ ,...n ]  
  
<column_name> ::=  
    { DELETED | INSERTED | from_table_name } . { * | column_name }  
    | $action  
```  
  
## <a name="arguments"></a>Argumentos

WITH \<common_table_expression>  
Especifica a exibição ou o conjunto de resultados nomeado temporário, também conhecido como expressão de tabela comum, que é definida no escopo da instrução MERGE. O conjunto de resultados deriva de uma consulta simples e é referenciado pela instrução MERGE. Para obter mais informações, confira [WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
TOP ( *expression* ) [ PERCENT ]  
Especifica o número ou a porcentagem de linhas afetadas. *expression* pode ser um número ou um percentual das linhas. As linhas referenciadas na expressão TOP não são organizadas em nenhuma ordem. Para obter mais informações, confira [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md).  
  
A cláusula TOP aplica-se depois que toda a tabela de origem e toda a tabela de destino são unidas e as linhas unidas que não se qualificam para uma ação de inserção, atualização ou exclusão são removidas. A cláusula TOP ainda reduz o número de linhas unidas para o valor especificado. As ações de inserção, atualização ou exclusão aplicam-se às linhas unidas restantes de maneira não ordenada. Ou seja, não há ordem na qual as linhas são distribuídas entre as ações definidas nas cláusulas WHEN. Por exemplo, a especificação de TOP (10) afeta 10 linhas. Dessas linhas, 7 podem ser atualizadas e 3 inseridas, ou 1 pode ser excluída, 5 atualizadas e 4 inseridas, e assim por diante.  
  
Como a instrução MERGE executa uma verificação de tabela completa das tabelas de origem e de destino, o desempenho de E/S às vezes é afetado quando se usa a cláusula TOP para modificar uma tabela grande criando vários lotes. Nesse cenário, é importante garantir que todos os lotes sucessivos se destinem a novas linhas.  
  
*database_name*  
O nome do banco de dados no qual *target_table* está localizado.  
  
*schema_name*  
O nome do esquema ao qual *target_table* pertence.  
  
*target_table*  
A tabela ou exibição em relação à qual as linhas de dados de \<table_source> são correspondidas com base na \<clause_search_condition>. *target_table* é o destino de qualquer operação de inserção, atualização ou exclusão especificada pelas cláusulas WHEN da instrução MERGE.  
  
Se *target_table* for uma exibição, qualquer ação com ela deverá atender às condições para atualizar exibições. Para obter mais informações, confira [Modificar dados por meio de uma exibição](../../relational-databases/views/modify-data-through-a-view.md).  
  
*target_table* não pode ser uma tabela remota. *target_table* não pode ter regras definidas nela.  
  
[ AS ] *table_alias*  
Um nome alternativo para fazer referência a uma tabela.  
  
USING \<table_source>  
Especifica a fonte de dados que é compatível com as linhas de dados em *target_table* com base em \<merge_search condition>. O resultado dessa correspondência dita as ações a serem tomadas pelas cláusulas WHEN da instrução MERGE. \<table_source> pode ser uma tabela remota ou uma tabela derivada que acessa tabelas remotas.
  
\<table_source> pode ser uma tabela derivada que usa o [!INCLUDE[tsql](../../includes/tsql-md.md)] [construtor de valor de tabela](../../t-sql/queries/table-value-constructor-transact-sql.md) para construir uma tabela especificando várias linhas.  
  
Para obter mais informações sobre a sintaxe e os argumentos dessa cláusula, veja [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md).  
  
ON \<merge_search_condition>  
Especifica as condições nas quais \<table_source> se une a *target_table* para determinar em que pontos há correspondências.
  
> [!CAUTION]  
> É importante especificar apenas as colunas da tabela de destino a serem usadas para fins de correspondência. Ou seja, especifique as colunas da tabela de destino que são comparadas à coluna correspondente da tabela de origem. Não tente melhorar o desempenho de consulta descartando linhas da tabela de destino na cláusula ON; por exemplo, especificando `AND NOT target_table.column_x = value`. Isso pode retornar resultados inesperados e incorretos.  
  
WHEN MATCHED THEN \<merge_matched>  
Especifica que todas as linhas de *target_table, que correspondem às linhas retornadas por \<table_source> ON \<merge_search_condition> e atendem a qualquer condição de pesquisa adicional, são atualizadas ou excluídas de acordo com a cláusula \<merge_matched>.  
  
A instrução MERGE pode ter, no máximo, duas cláusulas WHEN MATCHED. Se duas cláusulas forem especificadas, a primeira deverá ser acompanhada de uma cláusula AND \<search_condition>. Para qualquer linha especificada, a segunda cláusula WHEN MATCHED será aplicada somente se a primeira não for. Se houver duas cláusulas WHEN MATCHED, uma delas deverá especificar uma ação UPDATE e a outra, uma ação DELETE. Quando UPDATE for especificada na cláusula \<merge_matched> e mais de uma linha de \<table_source> corresponder a uma linha em *target_table* com base em \<merge_search_condition>, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará um erro. A instrução MERGE não pode atualizar a mesma linha mais de uma vez, nem atualizar e excluir a mesma linha.  
  
WHEN NOT MATCHED [ BY TARGET ] THEN \<merge_not_matched>  
Especifica que uma linha é inserida em *target_table* para cada linha retornada por \<table_source> ON \<merge_search_condition> que não corresponde a uma linha em *target_table*, mas atende a um condição de pesquisa adicional, se houver. Os valores a serem inseridos são especificados pela cláusula \<merge_not_matched>. A instrução MERGE só pode ter uma cláusula WHEN NOT MATCHED [ BY TARGET ].

WHEN NOT MATCHED BY SOURCE THEN \<merge_matched>  
Especifica que todas as linhas de *target_table que não correspondem às linhas retornadas por \<table_source> ON \<merge_search_condition> e atendem a qualquer condição de pesquisa adicional são atualizadas ou excluídas de acordo com a cláusula \<merge_matched>.  
  
A instrução MERGE pode ter, no máximo, duas cláusulas WHEN NOT MATCHED BY SOURCE. Se forem especificadas duas cláusulas, a primeira deverá ser acompanhada por uma cláusula AND \<clause_search_condition>. Para qualquer linha especificada, a segunda cláusula WHEN NOT MATCHED BY SOURCE será aplicada somente se a primeira não for. Se houver duas cláusulas WHEN NOT MATCHED BY SOURCE, uma delas deverá especificar uma ação UPDATE e a outra, uma ação DELETE. Somente as colunas da tabela de destino podem ser referenciadas na \<clause_search_condition>.  
  
Quando nenhuma linha é retornada por \<table_source>, não é possível acessar as colunas na tabela de origem. Se a ação de atualização ou exclusão especificada na cláusula \<merge_matched> referenciar colunas na tabela de origem, o erro 207 (Nome de coluna inválido) será retornado. Por exemplo, a cláusula `WHEN NOT MATCHED BY SOURCE THEN UPDATE SET TargetTable.Col1 = SourceTable.Col1` pode fazer a instrução falhar porque não é possível acessar `Col1` na tabela de origem.  
  
AND \<clause_search_condition>  
Especifica qualquer critério de pesquisa válido. Para obter mais informações, consulte [Condição de pesquisa &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
\<table_hint_limited>  
Especifica uma ou mais dicas de tabela a serem aplicadas à tabela de destino para cada uma das ações de inserção, atualização ou exclusão executadas pela instrução MERGE. A palavra-chave WITH e parênteses são necessários.  
  
NOLOCK e READUNCOMMITTED não são permitidas. Para obter mais informações sobre dicas de tabela, consulte [Dicas de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
Especificar a dica TABLOCK em uma tabela que é o destino de uma instrução INSERT tem o mesmo efeito de especificar a dica TABLOCKX. Um bloqueio exclusivo é obtido na tabela. Quando FORCESEEK é especificada, ela se aplica a uma instância implícita da tabela de destino unida à tabela de origem.  
  
> [!CAUTION]  
> Especificar READPAST com WHEN NOT MATCHED [ BY TARGET ] THEN INSERT pode resultar em operações INSERT que violam restrições UNIQUE.  
  
INDEX ( index_val [ ,...n ] )  
Especifica o nome ou a ID de um ou mais índices na tabela de destino para a execução de uma união implícita à tabela de origem. Para obter mais informações, consulte [Dicas de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
\<output_clause>  
Retorna uma linha para cada linha de *target_table* que é atualizada, inserida ou excluída, sem nenhuma ordem específica. **$action** pode ser especificada na cláusula output. **$action** é uma coluna do tipo **nvarchar(10)** que retorna um dos três valores para cada linha: 'INSERT', 'UPDATE' ou 'DELETE', de acordo com a ação executada na linha. Para obter mais informações sobre os argumentos dessa cláusula, veja [Cláusula OUTPUT &#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md).  
  
OPTION ( \<query_hint> [ ,...n ] )  
Especifica que dicas do otimizador são usadas para personalizar o modo como o Mecanismo de Banco de Dados processa a instrução. Para obter mais informações, veja [Dicas de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
\<merge_matched>  
Especifica a ação de atualização ou exclusão que é aplicada a todas as linhas de *target_table* que não correspondem às linhas retornadas por \<table_source> ON \<merge_search_condition> e atendem a qualquer condição de pesquisa adicional.  
  
UPDATE SET \<set_clause>  
Especifica a lista de nomes de colunas ou de variáveis a serem atualizados na tabela de destino e os valores com os quais eles devem ser atualizados.  
  
Para obter mais informações sobre os argumentos dessa cláusula, veja [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md). Não é permitido definir uma variável com o mesmo valor de uma coluna.  
  
Delete (excluir)  
Especifica que as linhas que correspondem a linhas em *target_table* são excluídas.  
  
\<merge_not_matched>  
Especifica os valores a serem inseridos na tabela de destino.  
  
(*column_list*)  
Uma lista de uma ou mais colunas da tabela de destino na qual inserir dados. As colunas devem ser especificadas como um nome de parte única. Caso contrário, haverá falha na instrução MERGE. *column_list* deve ser colocada entre parênteses e separada por vírgulas.  
  
VALUES ( *values_list*)  
Uma lista de constantes, variáveis ou expressões separadas por vírgulas que retorna valores a serem inseridos na tabela de destino. As expressões não podem conter uma instrução EXECUTE.  
  
DEFAULT VALUES  
Força a linha inserida a conter os valores padrão definidos para cada coluna.  
  
Para obter mais informações sobre essa cláusula, veja [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md).  
  
\<search condition>  
Especifica os critérios de pesquisa para especificar \<merge_search_condition> ou \<clause_search_condition>. Para obter mais informações sobre os argumentos para essa cláusula, veja [Condição de pesquisa &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md).  

\<graph search pattern>  
Especifica o padrão de correspondência do grafo. Para obter mais informações sobre os argumentos dessa cláusula, consulte [MATCH &#40;Transact-SQL&#41;](../../t-sql/queries/match-sql-graph.md)
  
## <a name="remarks"></a>Remarks

Pelo menos uma das três cláusulas MATCHED devem ser especificadas, mas elas podem ser especificadas em qualquer ordem. Uma variável não pode ser atualizada mais de uma vez na mesma cláusula MATCHED.  
  
Qualquer ação de inserção, atualização ou exclusão especificada na tabela de destino pela instrução MERGE é limitada pelas restrições definidas nela, incluindo qualquer restrição de integridade referencial em cascata. Se IGNORE_DUP_KEY for ON em qualquer índice exclusivo na tabela de destino, MERGE vai ignorar essa configuração.  
  
A instrução MERGE exige um ponto-e-vírgula (;) como terminador de instrução. O erro 10713 ocorre quando uma instrução MERGE é executada sem o terminador.  
  
Quando usada depois de MERGE, [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md) retorna o número total de linhas inseridas, atualizadas e excluídas para o cliente.  
  
MERGE é uma palavra-chave totalmente reservada quando o nível de compatibilidade do banco de dados é definido como 100 ou superior. A instrução MERGE está disponível abaixo dos níveis de compatibilidade do banco de dados 90 e 100. No entanto, a palavra-chave não é totalmente reservada quando o nível de compatibilidade do banco de dados está definido como 90.  
  
Não use a instrução **MERGE** com a replicação de atualização enfileirada. A instrução **MERGE** e o gatilho de atualização enfileirada não são compatíveis. Substitua a instrução **MERGE** por uma instrução de inserção ou de atualização.  
  
## <a name="trigger-implementation"></a>Implementação de gatilho

Para cada ação de inserção, atualização ou exclusão especificada na instrução MERGE, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dispara qualquer gatilho AFTER correspondente definido na tabela de destino, mas não garante em qual ação os gatilhos serão disparados primeiro ou por último. Os gatilhos definidos para a mesma ação respeitam a ordem que você especifica. Para obter mais informações sobre a configuração da ordem de acionamento do gatilho, veja [Especificar o primeiro e o último gatilho](../../relational-databases/triggers/specify-first-and-last-triggers.md).  
  
Se a tabela de destino tiver um gatilho INSTEAD OF habilitado definido para uma ação de inserção, atualização ou exclusão realizada por uma instrução MERGE, ela deverá ter um gatilho INSTEAD OF habilitado para todas as ações especificadas na instrução MERGE.  
  
Se algum gatilho INSTEAD OF UPDATE ou INSTEAD OF DELETE for definido em *target_table*, as operações de atualização ou de exclusão não serão executadas. Em vez disso, os gatilhos serão disparados e as tabelas **inserted** e **deleted** serão populadas adequadamente.  
  
Se algum gatilho INSTEAD OF INSERT for definido em *target_table*, a operação de inserção não será executada. Em vez disso, a tabela será populada adequadamente.  
  
## <a name="permissions"></a>Permissões

Requer a permissão SELECT na tabela de origem e as permissões INSERT, UPDATE ou DELETE na tabela de destino. Para saber mais, confira a seção Permissões nos artigos [SELECT](../../t-sql/queries/select-transact-sql.md), [INSERT](../../t-sql/statements/insert-transact-sql.md), [UPDATE](../../t-sql/queries/update-transact-sql.md) e [DELETE](../../t-sql/statements/delete-transact-sql.md).  
  
## <a name="optimizing-merge-statement-performance"></a>Otimizar o desempenho da instrução MERGE

Ao usar a instrução MERGE, você pode substituir as instruções DML individuais por uma única instrução. Isso melhora o desempenho das consultas porque as operações são executadas em uma única instrução, diminuindo o número de vezes que os dados das tabelas de origem e de destino são processados. No entanto, os ganhos de desempenho dependem do uso de índices e junções corretos e de outras considerações.

### <a name="index-best-practices"></a>Melhores práticas de índice

Para melhorar o desempenho da instrução MERGE, é recomendável seguir estas diretrizes de índice:

- Crie um índice com base nas colunas de junção da tabela de origem que seja exclusivo e abrangente.
- Crie um índice clusterizado exclusivo com base nas colunas de junção da tabela de destino.

Esses índices asseguram que as chaves de junção sejam exclusivas e que os dados das tabelas sejam classificados. O desempenho das consultas é aprimorado porque o otimizador de consulta não precisa executar processamento de validação extra para localizar e atualizar linhas duplicadas, e não há necessidade de operações de suporte adicionais.

### <a name="join-best-practices"></a>Melhores práticas de JOIN

Para melhorar o desempenho da instrução MERGE e assegurar a obtenção dos resultados corretos, é recomendável seguir estas diretrizes de junção:

- Especifique apenas condições de pesquisa na cláusula ON <merge_search_condition> que determinem os critérios para corresponder dados nas tabelas de origem e de destino. Ou seja, especifique apenas as colunas da tabela de destino que são comparadas com as colunas correspondentes da tabela de origem. 
- Não inclua comparações com outros valores, como uma constante.

Para filtrar linhas das tabelas de origem ou de destino, use um dos métodos a seguir.

- Especifique o critério de pesquisa para filtragem de linhas na cláusula WHEN apropriada. Por exemplo, WHEN NOT MATCHED AND S.EmployeeName LIKE 'S%' THEN INSERT....
- Defina uma exibição na origem ou no destino que retorne as linhas filtradas e faça referência à exibição como a tabela de origem ou de destino. Se a exibição for definida na tabela de destino, quaisquer ações sobre ela terão que atender às condições para atualização das exibições. Para obter mais informações sobre como atualizar dados usando uma exibição, consulte Modificar dados por meio de uma exibição.
- Use a cláusula `WITH <common table expression>` para filtrar linhas das tabelas de origem e de destino. Esse método é semelhante a especificar critérios adicionais de pesquisa na cláusula ON e pode produzir resultados incorretos. É recomendável evitar o uso desse método ou testá-lo criteriosamente antes de implementá-lo.

A operação de junção na instrução MERGE é otimizada da mesma forma que uma junção na instrução SELECT. Ou seja, quando o SQL Server processa junções, o otimizador de consulta escolhe o método mais eficaz (entre várias possibilidades) de processamento da junção. Quando a origem e o destino têm tamanho semelhante e as diretrizes de índice descritas anteriormente são aplicadas às tabelas de origem e de destino, um operador merge join é o plano de consulta mais eficiente. Isso porque ambas as tabelas são examinadas uma vez e não há necessidade de classificar os dados. Quando a tabela de origem é menor do que a de destino, é preferível usar um operador nested loops.

Você pode forçar o uso de determinada junção especificando a cláusula `OPTION (<query_hint>)` na instrução MERGE. É recomendável não usar a junção hash como dica de consulta para instruções MERGE, pois esse tipo de junção não usa índices.

### <a name="parameterization-best-practices"></a>Melhores práticas de parametrização

Se uma instrução SELECT, INSERT, UPDATE ou DELETE for executada sem parâmetros, o otimizador de consulta do SQL Server poderá parametrizar a instrução internamente. Isso significa que qualquer valor literal contido na consulta é substituído por parâmetros. Por exemplo, a instrução INSERT dbo.MyTable (Col1, Col2) VALUES (1, 10), pode ser implementada internamente como INSERT dbo.MyTable (Col1, Col2) VALUES (@p1, @p2). Esse processo, chamado de parametrização simples, aumenta a capacidade do mecanismo relacional de comparar as novas instruções SQL com planos de execução existentes anteriormente compilados. O desempenho da consulta pode ser melhorado porque a frequência das compilações e recompilações de consulta é reduzida. O otimizador de consulta não aplica o processo de parametrização simples a instruções MERGE. Por isso, as instruções MERGE que contêm valores literais podem não ter um desempenho tão bom quanto as instruções INSERT, UPDATE ou DELETE individuais, pois um novo plano é compilado sempre que a instrução MERGE é executada.

Para melhorar o desempenho da consulta, é recomendável seguir estas diretrizes de parametrização:

- Parametrize todos os valores literais na cláusula `ON <merge_search_condition>` e nas cláusulas `WHEN` da instrução MERGE. Por exemplo, você pode inserir a instrução MERGE a um procedimento armazenado que substitua os valores literais por parâmetros de entrada apropriados.
- Se você não conseguir parametrizar a instrução, crie um guia de plano do tipo `TEMPLATE` e especifique a dica de consulta `PARAMETERIZATION FORCED` no guia de plano.
- Se instruções MERGE forem executadas com frequência no banco de dados, considere definir a opção PARAMETERIZATION no banco de dados como FORCED. Tome cuidado quando for definir essa opção. A opção `PARAMETERIZATION` é uma configuração de banco de dados e afeta a maneira como são processadas todas as consultas feitas nele.

### <a name="top-clause-best-practices"></a>Melhores práticas da cláusula TOP

Na instrução MERGE, a cláusula TOP especifica o número ou a porcentagem de linhas que são afetadas depois que as tabelas de origem e de destino são unidas e que as linhas que não se qualificam para uma ação de inserção, atualização ou exclusão são removidas. A cláusula TOP ainda reduz o número de linhas unidas para o valor especificado e as ações de inserção, atualização ou exclusão são aplicadas às linhas unidas restantes de uma forma não ordenada. Ou seja, não há nenhuma ordem na qual as linhas são distribuídas entre as ações definidas nas cláusulas WHEN. Por exemplo, especificar TOP (10) afeta dez linhas. Dessas linhas, sete podem ser atualizadas e três inseridas, ou uma pode ser excluída, cinco atualizadas e quatro inseridas etc.

É comum usar a cláusula TOP para executar operações DML (linguagem de manipulação de dados) em uma tabela grande em lotes. Quando se usa a cláusula TOP na instrução MERGE para esta finalidade, é importante entender as implicações a seguir.

- O desempenho de E/S poderá ser afetado.

  A instrução MERGE faz uma verificação completa das tabelas de origem e de destino. Dividir a operação em lotes diminui o número de operações de gravação executadas por lote; no entanto, cada lote fará uma verificação completa das tabelas de origem e de destino. A atividade de leitura resultante poderá afetar o desempenho da consulta.

- Pode haver resultados incorretos.

  É importante assegurar que todos os lotes em sucessão visem as novas linhas; do contrário, poderão ocorrer comportamentos indesejados, como inserção incorreta de linhas duplicadas na tabela de destino. Isso pode acontecer quando a tabela de origem inclui uma linha que não estava em um lote de destino, mas que estava na tabela de destino global.

- Para assegurar resultados corretos:

  - Use a cláusula ON para determinar quais linhas de origem afetam linhas de destino existentes e quais são genuinamente novas.
  - Use uma condição adicional na cláusula WHEN MATCHED para determinar se a linha de destino já foi atualizada por um lote anterior.

Como a cláusula TOP só é aplicada depois que essas cláusulas são aplicadas, cada execução insere uma linha genuinamente não correspondente ou atualiza uma linha existente.

### <a name="bulk-load-best-practices"></a>Melhores práticas de carregamento em massa

A instrução MERGE pode ser usada para carregar com eficiência dados de carregamento em massa de um arquivo de dados de origem em uma tabela de destino especificando-se a cláusula `OPENROWSET(BULK…)` como tabela de origem. Dessa forma, o arquivo inteiro é processado em um único lote.

Para melhorar o desempenho do processo de mesclagem em lote, é recomendável seguir estas diretrizes:

- Crie um índice clusterizado com base nas colunas de junção da tabela de destino.
- Use as dicas ORDER e UNIQUE na cláusula `OPENROWSET(BULK…)` para especificar como o arquivo de dados de origem deverá ser classificado.

  Por padrão, a operação em massa presume que o arquivo de dados não está ordenado. Por isso, é importante que os dados de origem sejam classificados de acordo com o índice clusterizado na tabela de destino e que a dica ORDER seja usada para indicar a ordem, de modo que o otimizador de consulta possa gerar um plano de consulta mais eficaz. As dicas são validadas em tempo de execução; se o fluxo de dados não estiver de acordo com as dicas especificadas, ocorrerá um erro.

Essas diretrizes asseguram que as chaves de junção sejam exclusivas e que a ordem de classificação dos dados do arquivo de origem corresponda à da tabela de destino. O desempenho das consultas é aprimorado porque não há necessidade de executar operações de classificação adicionais e não são exigidas cópias de dados desnecessárias.

### <a name="measuring-and-diagnosing-merge-performance"></a>Avaliação e diagnóstico do desempenho de MERGE

Os recursos a seguir estão disponíveis para ajudar você a avaliar e diagnosticar o desempenho de instruções MERGE.

- Use o contador merge stmt na exibição de gerenciamento dinâmico [sys.dm_exec_query_optimizer_info](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-optimizer-info-transact-sql.md) para retornar o número de otimizações de consulta relativas a instruções MERGE.
- Use o atributo merge_action_type na exibição de gerenciamento dinâmico [sys.dm_exec_plan_attributes](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md) para retornar o tipo de plano de execução de gatilho usado como resultado de uma instrução MERGE.
- Use o Rastreamento do SQL para coletar dados de solução de problemas para a instrução MERGE da mesma forma que você faria para outras instruções DML. Para obter mais informações, consulte [SQL Trace](../../relational-databases/sql-trace/sql-trace.md).

## <a name="examples"></a>Exemplos  

### <a name="a-using-merge-to-do-insert-and-update-operations-on-a-table-in-a-single-statement"></a>A. Usar MERGE para executar operações INSERT e UPDATE em uma tabela em uma única instrução

Um cenário comum é atualizar uma ou mais colunas em uma tabela se existir uma linha correspondente. Ou inserir os dados como uma nova linha se uma linha correspondente não existir. Normalmente, seja qual for o cenário, você transmite parâmetros para um procedimento armazenado que contém as instruções UPDATE e INSERT apropriadas. Com a instrução MERGE, você pode executar as duas tarefas em uma única instrução. O exemplo a seguir mostra um procedimento armazenado no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] que contém as instruções INSERT e UPDATE. O procedimento é então modificado para executar as operações equivalentes usando uma única instrução MERGE.  
  
```sql  
CREATE PROCEDURE dbo.InsertUnitMeasure  
    @UnitMeasureCode nchar(3),  
    @Name nvarchar(25)  
AS
BEGIN  
    SET NOCOUNT ON;  
-- Update the row if it exists.
    UPDATE Production.UnitMeasure  
SET Name = @Name  
WHERE UnitMeasureCode = @UnitMeasureCode  
-- Insert the row if the UPDATE statement failed.  
IF (@@ROWCOUNT = 0 )  
BEGIN  
    INSERT INTO Production.UnitMeasure (UnitMeasureCode, Name)  
    VALUES (@UnitMeasureCode, @Name)  
END  
END;  
GO  
-- Test the procedure and return the results.  
EXEC InsertUnitMeasure @UnitMeasureCode = 'ABC', @Name = 'Test Value';  
SELECT UnitMeasureCode, Name FROM Production.UnitMeasure  
WHERE UnitMeasureCode = 'ABC';  
GO  
  
-- Rewrite the procedure to perform the same operations using the
-- MERGE statement.  
-- Create a temporary table to hold the updated or inserted values
-- from the OUTPUT clause.  
CREATE TABLE #MyTempTable  
    (ExistingCode nchar(3),  
     ExistingName nvarchar(50),  
     ExistingDate datetime,  
     ActionTaken nvarchar(10),  
     NewCode nchar(3),  
     NewName nvarchar(50),  
     NewDate datetime  
    );  
GO  
ALTER PROCEDURE dbo.InsertUnitMeasure  
    @UnitMeasureCode nchar(3),  
    @Name nvarchar(25)  
AS
BEGIN  
    SET NOCOUNT ON;  
  
    MERGE Production.UnitMeasure AS target  
    USING (SELECT @UnitMeasureCode, @Name) AS source (UnitMeasureCode, Name)  
    ON (target.UnitMeasureCode = source.UnitMeasureCode)  
    WHEN MATCHED THEN
        UPDATE SET Name = source.Name  
    WHEN NOT MATCHED THEN  
        INSERT (UnitMeasureCode, Name)  
        VALUES (source.UnitMeasureCode, source.Name)  
    OUTPUT deleted.*, $action, inserted.* INTO #MyTempTable;  
END;  
GO  
-- Test the procedure and return the results.  
EXEC InsertUnitMeasure @UnitMeasureCode = 'ABC', @Name = 'New Test Value';  
EXEC InsertUnitMeasure @UnitMeasureCode = 'XYZ', @Name = 'Test Value';  
EXEC InsertUnitMeasure @UnitMeasureCode = 'ABC', @Name = 'Another Test Value';  
  
SELECT * FROM #MyTempTable;  
-- Cleanup
DELETE FROM Production.UnitMeasure WHERE UnitMeasureCode IN ('ABC','XYZ');  
DROP TABLE #MyTempTable;  
GO  
```  
  
### <a name="b-using-merge-to-do-update-and-delete-operations-on-a-table-in-a-single-statement"></a>B. Usar MERGE para executar as operações UPDATE e DELETE em uma tabela em uma única instrução

O exemplo a seguir usa MERGE para atualizar diariamente a tabela `ProductInventory` no banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] com base em pedidos processados na tabela `SalesOrderDetail`. A coluna `Quantity` da tabela `ProductInventory` foi atualizada subtraindo o número de pedidos colocados a cada dia para cada produto na tabela `SalesOrderDetail`. Se o número de pedidos de um produto reduzir o nível de estoque de um produto para 0 ou menos, a linha desse produto será excluída da tabela `ProductInventory`.  
  
```sql  
CREATE PROCEDURE Production.usp_UpdateInventory  
    @OrderDate datetime  
AS  
MERGE Production.ProductInventory AS target  
USING (SELECT ProductID, SUM(OrderQty) FROM Sales.SalesOrderDetail AS sod  
    JOIN Sales.SalesOrderHeader AS soh  
    ON sod.SalesOrderID = soh.SalesOrderID  
    AND soh.OrderDate = @OrderDate  
    GROUP BY ProductID) AS source (ProductID, OrderQty)  
ON (target.ProductID = source.ProductID)  
WHEN MATCHED AND target.Quantity - source.OrderQty <= 0  
    THEN DELETE  
WHEN MATCHED
    THEN UPDATE SET target.Quantity = target.Quantity - source.OrderQty,
                    target.ModifiedDate = GETDATE()  
OUTPUT $action, Inserted.ProductID, Inserted.Quantity,
    Inserted.ModifiedDate, Deleted.ProductID,  
    Deleted.Quantity, Deleted.ModifiedDate;  
GO  
  
EXECUTE Production.usp_UpdateInventory '20030501'  
```  
  
### <a name="c-using-merge-to-do-update-and-insert-operations-on-a-target-table-by-using-a-derived-source-table"></a>C. Usar MERGE para executar as operações UPDATE e INSERT em uma tabela de destino usando uma tabela de origem derivada

O exemplo a seguir usa MERGE para modificar a tabela `SalesReason` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] atualizando ou inserindo linhas. Quando o valor de `NewName` na tabela de origem corresponde a um valor na coluna `Name` da tabela de destino (`SalesReason`), a coluna `ReasonType` é atualizada na tabela de destino. Quando o valor de `NewName` não corresponde, a linha de origem é inserida na tabela de destino. A tabela de origem é uma tabela derivada que usa o construtor de valor de tabela do [!INCLUDE[tsql](../../includes/tsql-md.md)] para especificar várias linhas para a tabela de origem. Para obter mais informações sobre como usar o construtor de valor de tabela em uma tabela derivada, veja [Construtor de valor de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/table-value-constructor-transact-sql.md). O exemplo também mostra como armazenar os resultados da cláusula OUTPUT em uma variável de tabela. E, em seguida, você resume os resultados da instrução MERGE executando uma operação de seleção simples que retorna a contagem de linhas inseridas e atualizadas.  
  
```sql  
-- Create a temporary table variable to hold the output actions.  
DECLARE @SummaryOfChanges TABLE(Change VARCHAR(20));  
  
MERGE INTO Sales.SalesReason AS Target  
USING (VALUES ('Recommendation','Other'), ('Review', 'Marketing'),
              ('Internet', 'Promotion'))  
       AS Source (NewName, NewReasonType)  
ON Target.Name = Source.NewName  
WHEN MATCHED THEN  
UPDATE SET ReasonType = Source.NewReasonType  
WHEN NOT MATCHED BY TARGET THEN  
INSERT (Name, ReasonType) VALUES (NewName, NewReasonType)  
OUTPUT $action INTO @SummaryOfChanges;  
  
-- Query the results of the table variable.  
SELECT Change, COUNT(*) AS CountPerChange  
FROM @SummaryOfChanges  
GROUP BY Change;  
```  
  
### <a name="d-inserting-the-results-of-the-merge-statement-into-another-table"></a>D. Inserindo os resultados da instrução MERGE em outra tabela

O exemplo a seguir captura dados retornados da cláusula OUTPUT de uma instrução MERGE e insere esses dados em outra tabela. A instrução MERGE atualiza diariamente a coluna `Quantity` da tabela `ProductInventory` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] com base em pedidos processados na tabela `SalesOrderDetail`. O exemplo captura as linhas atualizadas e as insere em outra tabela que é usada para rastrear as alterações do estoque.  
  
```sql  
CREATE TABLE Production.UpdatedInventory  
    (ProductID INT NOT NULL, LocationID int, NewQty int, PreviousQty int,  
     CONSTRAINT PK_Inventory PRIMARY KEY CLUSTERED (ProductID, LocationID));  
GO  
INSERT INTO Production.UpdatedInventory  
SELECT ProductID, LocationID, NewQty, PreviousQty
FROM  
(    MERGE Production.ProductInventory AS pi  
     USING (SELECT ProductID, SUM(OrderQty)
            FROM Sales.SalesOrderDetail AS sod  
            JOIN Sales.SalesOrderHeader AS soh  
            ON sod.SalesOrderID = soh.SalesOrderID  
            AND soh.OrderDate BETWEEN '20030701' AND '20030731'  
            GROUP BY ProductID) AS src (ProductID, OrderQty)  
     ON pi.ProductID = src.ProductID  
    WHEN MATCHED AND pi.Quantity - src.OrderQty >= 0
        THEN UPDATE SET pi.Quantity = pi.Quantity - src.OrderQty  
    WHEN MATCHED AND pi.Quantity - src.OrderQty <= 0
        THEN DELETE  
    OUTPUT $action, Inserted.ProductID, Inserted.LocationID,
        Inserted.Quantity AS NewQty, Deleted.Quantity AS PreviousQty)  
 AS Changes (Action, ProductID, LocationID, NewQty, PreviousQty)
 WHERE Action = 'UPDATE';  
GO  
```  

### <a name="e-using-merge-to-do-insert-or-update-on-a-target-edge-table-in-a-graph-database"></a>E. Usar MERGE para executar INSERT ou UPDATE em uma tabela de borda de destino em um banco de dados de grafo

Neste exemplo, você cria tabelas de nó `Person` e `City` e uma tabela de borda `livesIn`. Você usa a instrução MERGE na borda `livesIn` para inserir uma nova linha se a borda ainda não existir entre um `Person` e `City`. Se a borda já existir, você apenas atualizará o atributo StreetAddress na borda `livesIn`.

```sql
-- CREATE node and edge tables
CREATE TABLE Person
    (
        ID INTEGER PRIMARY KEY,
        PersonName VARCHAR(100)
    )
AS NODE
GO

CREATE TABLE City
    (
        ID INTEGER PRIMARY KEY,
        CityName VARCHAR(100),
        StateName VARCHAR(100)
    )
AS NODE
GO

CREATE TABLE livesIn
    (
        StreetAddress VARCHAR(100)
    )
AS EDGE
GO

-- INSERT some test data into node and edge tables
INSERT INTO Person VALUES (1, 'Ron'), (2, 'David'), (3, 'Nancy')
GO

INSERT INTO City VALUES (1, 'Redmond', 'Washington'), (2, 'Seattle', 'Washington')
GO

INSERT livesIn SELECT P.$node_id, C.$node_id, c
FROM Person P, City C, (values (1,1, '123 Avenue'), (2,2,'Main Street')) v(a,b,c)
WHERE P.id = a AND C.id = b
GO

-- Use MERGE to update/insert edge data
CREATE OR ALTER PROCEDURE mergeEdge
    @PersonId integer,
    @CityId integer,
    @StreetAddress varchar(100)
AS
BEGIN
    MERGE livesIn
        USING ((SELECT @PersonId, @CityId, @StreetAddress) AS T (PersonId, CityId, StreetAddress)
                JOIN Person ON T.PersonId = Person.ID
                JOIN City ON T.CityId = City.ID)
        ON MATCH (Person-(livesIn)->City)
    WHEN MATCHED THEN
        UPDATE SET StreetAddress = @StreetAddress
    WHEN NOT MATCHED THEN
        INSERT ($from_id, $to_id, StreetAddress)
        VALUES (Person.$node_id, City.$node_id, @StreetAddress) ;
END
GO

-- Following will insert a new edge in the livesIn edge table
EXEC mergeEdge 3, 2, '4444th Avenue'
GO

-- Following will update the StreetAddress on the edge that connects Ron to Redmond
EXEC mergeEdge 1, 1, '321 Avenue'
GO

-- Verify that all the address were added/updated correctly
SELECT PersonName, CityName, StreetAddress
FROM Person , City , livesIn
WHERE MATCH(Person-(livesIn)->city)
GO
```
  
## <a name="see-also"></a>Consulte Também

- [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)
- [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)
- [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)
- [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)
- [Cláusula OUTPUT &#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md)
- [MERGE em pacotes do Integration Services](../../integration-services/control-flow/merge-in-integration-services-packages.md)
- [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)
- [Construtor de valor de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/table-value-constructor-transact-sql.md)  
