---
title: FROM (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- JOIN
- FROM_TSQL
- FROM
- JOIN_TSQL
- CROSS_TSQL
- CROSS_APPLY_TSQL
- APPLY_TSQL
- CROSS_JOIN_TSQL
dev_langs: TSQL
helpviewer_keywords:
- OUTER APPLY operator
- hints [SQL Server], FROM clause
- SELECT statement [SQL Server], FROM clause
- ISO syntax
- DELETE statement [SQL Server], FROM clause
- CROSS APPLY operator
- FROM clause
- APPLY operator
- joins [SQL Server], FROM clause
- UPDATE statement [SQL Server], FROM clause
- derived tables
ms.assetid: 36b19e68-94f6-4539-aeb1-79f5312e4263
caps.latest.revision: "97"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 9ddc3ee291d4e3b498dd6dfd9bbb49ca4299bea6
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="from-transact-sql"></a>FROM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Especifica as tabelas, exibições, tabelas derivadas e tabelas unidas usadas em instruções DELETE, SELECT e UPDATE no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Na instrução SELECT, a cláusula FROM é necessária, exceto quando a lista de seleção contém apenas constantes, variáveis e expressões aritméticas (sem nomes de coluna).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
[ FROM { <table_source> } [ ,...n ] ]   
<table_source> ::=   
{  
    table_or_view_name [ [ AS ] table_alias ]   
        [ <tablesample_clause> ]   
        [ WITH ( < table_hint > [ [ , ]...n ] ) ]   
    | rowset_function [ [ AS ] table_alias ]   
        [ ( bulk_column_alias [ ,...n ] ) ]   
    | user_defined_function [ [ AS ] table_alias ]  
    | OPENXML <openxml_clause>   
    | derived_table [ [ AS ] table_alias ] [ ( column_alias [ ,...n ] ) ]   
    | <joined_table>   
    | <pivoted_table>   
    | <unpivoted_table>  
    | @variable [ [ AS ] table_alias ]  
    | @variable.function_call ( expression [ ,...n ] )   
        [ [ AS ] table_alias ] [ (column_alias [ ,...n ] ) ]  
    | FOR SYSTEM_TIME <system_time>   
}  
<tablesample_clause> ::=  
    TABLESAMPLE [SYSTEM] ( sample_number [ PERCENT | ROWS ] )   
        [ REPEATABLE ( repeat_seed ) ]   
  
<joined_table> ::=   
{  
    <table_source> <join_type> <table_source> ON <search_condition>   
    | <table_source> CROSS JOIN <table_source>   
    | left_table_source { CROSS | OUTER } APPLY right_table_source   
    | [ ( ] <joined_table> [ ) ]   
}  
<join_type> ::=   
    [ { INNER | { { LEFT | RIGHT | FULL } [ OUTER ] } } [ <join_hint> ] ]  
    JOIN  
  
<pivoted_table> ::=  
    table_source PIVOT <pivot_clause> [ [ AS ] table_alias ]  
  
<pivot_clause> ::=  
        ( aggregate_function ( value_column [ [ , ]...n ])   
        FOR pivot_column   
        IN ( <column_list> )   
    )   
  
<unpivoted_table> ::=  
    table_source UNPIVOT <unpivot_clause> [ [ AS ] table_alias ]  
  
<unpivot_clause> ::=  
    ( value_column FOR pivot_column IN ( <column_list> ) )   
  
<column_list> ::=  
    column_name [ ,...n ]   
  
<system_time> ::=  
{  
       AS OF <date_time>  
    |  FROM <start_date_time> TO <end_date_time>  
    |  BETWEEN <start_date_time> AND <end_date_time>  
    |  CONTAINED IN (<start_date_time> , <end_date_time>)   
    |  ALL  
}  
  
    <date_time>::=  
        <date_time_literal> | @date_time_variable  
  
    <start_date_time>::=  
        <date_time_literal> | @date_time_variable  
  
    <end_date_time>::=  
        <date_time_literal> | @date_time_variable  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
FROM { <table_source> [ ,...n ] }  
  
<table_source> ::=   
{  
    [ database_name . [ schema_name ] . | schema_name . ] table_or_view_name [ AS ] table_or_view_alias  
    | derived_table [ AS ] table_alias [ ( column_alias [ ,...n ] ) ]  
    | <joined_table>  
}  
  
<joined_table> ::=   
{  
    <table_source> <join_type> <table_source> ON search_condition   
    | <table_source> CROSS JOIN <table_source> 
    | left_table_source { CROSS | OUTER } APPLY right_table_source   
    | [ ( ] <joined_table> [ ) ]   
}  
  
<join_type> ::=   
    [ INNER ] [ <join hint> ] JOIN  
    | LEFT  [ OUTER ] JOIN  
    | RIGHT [ OUTER ] JOIN  
    | FULL  [ OUTER ] JOIN  
  
<join_hint> ::=   
    REDUCE  
    | REPLICATE  
    | REDISTRIBUTE  
```  
  
## <a name="arguments"></a>Argumentos  
\<table_source>  
 Especifica uma tabela, exibição, variável de tabela ou origem de tabela derivada, com ou sem um alias, a ser usada na instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]. Até 256 origens da tabela podem ser usadas em uma instrução, embora o limite varie de acordo com a memória disponível e a complexidade de outras expressões na consulta. Consultas individuais podem não aceitar até 256 origens de tabela.  
  
> [!NOTE]  
>  O desempenho da consulta pode ser prejudicado com um grande número de tabelas referenciadas em uma consulta. O tempo de compilação e otimização também é afetado por outros fatores. Isso inclui a presença de índices e exibições indexadas em cada \<table_source > e o tamanho do \<select_list > na instrução SELECT.  
  
 A ordem de origens de tabela após a palavra-chave FROM não afeta o conjunto de resultados que é retornado. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna erros quando aparecem nomes duplicados na cláusula FROM.  
  
 *table_or_view_name*  
 É o nome de uma tabela ou exibição.  
  
 Se a tabela ou exibição existe em outro banco de dados na mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use um nome totalmente qualificado no formato *banco de dados*. *esquema*. *object_name*.  
  
 Se a tabela ou exibição existe fora da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]l, use um nome de quatro partes no formato *linked_server*. *catálogo*. *esquema*. *objeto*. Para obter mais informações, consulte [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md). Um nome de quatro partes que é construído usando o [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) funciona como a parte do nome do servidor também pode ser usada para especificar a origem da tabela remota. Quando OPENDATASOURCE é especificado, *database_name* e *schema_name* não podem ser aplicadas a todas as fontes de dados e está sujeita aos recursos do provedor OLE DB que acessa o objeto remoto.  
  
 [COMO] *table_alias*  
 É um alias para *table_source* que podem ser usados para conveniência ou para distinguir uma tabela ou exibição em uma autojunção ou subconsulta. Em geral, um alias é um nome de tabela abreviado usado para referência a colunas específicas das tabelas em uma junção. Se o nome da coluna existir em mais de uma tabela na junção, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exigirá que ele seja qualificado por um nome de tabela, nome de exibição ou alias. O nome da tabela não poderá ser usado se um alias estiver definido.  
  
 Quando uma tabela derivada, linhas ou função com valor de tabela ou na cláusula de operador (como PIVOT ou UNPIVOT) é usada, obrigatório *table_alias* no final da cláusula é o nome de tabela associado para todas as colunas, incluindo colunas de agrupamento retornado.  
  
 COM (\<table_hint >)  
 Especifica que o otimizador de consulta use uma estratégia de otimização ou bloqueio com esta tabela e para esta instrução. Para obter mais informações, consulte [Dicas de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 *rowset_function*  

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  

  
 Especifica uma das funções de conjunto de linhas, como OPENROWSET, que retorna um objeto que pode ser usado no lugar de uma referência de tabela. Para obter mais informações sobre uma lista de funções de conjunto de linhas, consulte [funções de conjunto de linhas &#40; Transact-SQL &#41; ](../../t-sql/functions/rowset-functions-transact-sql.md).  
  
 O uso das funções OPENROWSET e OPENQUERY para especificar que um objeto remoto depende dos recursos do provedor OLE DB que acessa o objeto.  
  
 *bulk_column_alias*  

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  

  
 É um alias opcional para substituir um nome de coluna no conjunto de resultados. Os aliases de coluna são permitidos somente em instruções SELECT que usam a função OPENROWSET com a opção BULK. Quando você usa *bulk_column_alias*, especifique um alias para cada coluna da tabela na mesma ordem em que as colunas no arquivo.  
  
> [!NOTE]  
>  Este alias substitui o atributo NAME nos elementos COLUMN de um arquivo de formato XML, se houver.  
  
 *user_defined_function*  
 Especifica uma função com valor de tabela.  
  
 OPENXML \<openxml_clause>  

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  

  
 Fornece uma exibição de conjunto de linhas em um documento XML. Para obter mais informações, consulte [OPENXML &#40; Transact-SQL &#41; ](../../t-sql/functions/openxml-transact-sql.md).  
  
 *derived_table*  
 É uma subconsulta que recupera linhas do banco de dados. *derived_table* é usado como entrada para a consulta externa.  
  
 *derivado* *_table* pode usar o [!INCLUDE[tsql](../../includes/tsql-md.md)] recurso do construtor de valor de tabela para especificar várias linhas. Por exemplo, `SELECT * FROM (VALUES (1, 2), (3, 4), (5, 6), (7, 8), (9, 10) ) AS MyTable(a, b);`. Para obter mais informações, consulte [construtor de valor de tabela &#40; Transact-SQL &#41; ](../../t-sql/queries/table-value-constructor-transact-sql.md).  
  
 *column_alias*  
 É um alias opcional para substituir um nome de coluna no conjunto de resultados da tabela derivada. Inclua um alias para cada coluna na lista de seleção e encerre a lista completa de aliases de coluna entre parênteses.  
  
 *table_or_view_name* FOR SYSTEM_TIME \<system_time >  

**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  

  
 Especifica que uma versão específica de dados é retornada da tabela temporal especificada e sua tabela de histórico de versão do sistema vinculado  
  
\<tablesample_clause>  
 Especifica que uma amostra de dados da tabela é retornada. A amostra pode ser aproximada. Esta cláusula pode ser usada em qualquer tabela primária ou unida em uma instrução SELECT, UPDATE ou DELETE. TABLESAMPLE não pode ser especificado com exibições.  
  
> [!NOTE]  
>  Quando você usa TABLESAMPLE em bancos de dados atualizados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o nível de compatibilidade do banco de dados é definido como 110 ou mais alto, PIVOT não é permitido em uma consulta CTE (expressão de tabela comum) recursiva. Para obter mais informações, veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
 SYSTEM  
 É um método de amostragem dependente de implementação especificado por padrões ISO. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esse é o único método de amostragem disponível e é aplicado por padrão. SYSTEM aplica um método de amostragem baseado em páginas em que um conjunto aleatório de páginas de uma tabela é escolhido para a amostra, e todas as linhas dessas páginas são retornadas como subconjunto da amostra.  
  
 *sample_number*  
 É uma expressão numérica constante exata ou aproximada que representa o percentual ou o número de linhas. Quando especificado com PERCENT, *sample_number* é convertido implicitamente em um **float** valor; caso contrário, ele será convertido em **bigint**. PERCENT é o padrão.  
  
 PERCENT  
 Especifica que um *sample_number* % das linhas da tabela deve ser recuperadas da tabela. Quando PERCENT é especificado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna um valor aproximado do percentual especificado. Quando PERCENT é especificado o *sample_number* expressão deve ser avaliada como um valor de 0 a 100.  
  
 ROWS  
 Especifica que, aproximadamente *sample_number* de linhas serão recuperados. Quando ROWS é especificado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna uma aproximação do número de linhas especificado. Quando ROWS é especificado, o *sample_number* expressão deve ser avaliada como um valor inteiro maior que zero.  
  
 REPEATABLE  
 Indica que a amostra selecionada pode ser retornada novamente. Quando especificado com o mesmo *repeat_seed* valor, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará o mesmo subconjunto de linhas como sem alterações foram feitas para quaisquer linhas na tabela. Quando especificado com outro *repeat_seed* valor, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será provavelmente retornará alguma amostra diferente das linhas na tabela. As seguintes ações na tabela são consideradas alterações: inserir, atualizar, excluir, recompilação do índice ou desfragmentação e restauração ou anexação do banco de dados.  
  
 *repeat_seed*  
 É uma expressão de inteiro constante usada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para gerar um número aleatório. *repeat_seed* é **bigint**. Se *repeat_seed* não for especificado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atribui um valor aleatório. Para um determinado *repeat_seed* valor, o resultado da amostragem é sempre o mesmo se nenhuma alteração tiverem sido aplicadas à tabela. O *repeat_seed* expressão deve ser avaliada como um inteiro maior que zero.  
  
 \<joined_table>  
 É um conjunto de resultados que é o produto de duas ou mais tabelas. Para várias junções, use parênteses para alterar a ordem natural das junções.  
  
\<join_type>  
 Especifica o tipo de operação de junção.  
  
 **INTERNA**  
 Especifica todos os pares de linhas correspondentes retornados. Descarta as linhas não correspondentes de ambas as tabelas. Quando nenhum tipo de junção é especificado, este é o padrão.  
  
 FULL [ OUTER ]  
 Especifica que uma linha da tabela esquerda ou direita que não atende à condição de junção seja incluída no conjunto de resultados, e as colunas de saída correspondentes à outra tabela sejam definidas como NULL. Isso ocorre além de todas as linhas normalmente retornadas por INNER JOIN.  
  
 LEFT [ OUTER ]  
 Especifica que todas as linhas da tabela esquerda que não atendem à condição de junção sejam incluídas no conjunto de resultados, e as colunas de saída da outra tabela sejam definidas como NULL além de todas as linhas retornadas pela junção interna.  
  
 RIGHT [OUTER]  
 Especifica que todas as linhas da tabela direita que não atendem à condição de junção sejam incluídas no conjunto de resultados, e as colunas de saída que correspondem à outra tabela sejam definidas como NULL, além de todas as linhas retornadas pela junção interna.  
  
\<join_hint>  
 Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDS](../../includes/sssds-md.md)], especifica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consulta otimizador usar uma dica de junção ou algoritmo de execução, por associação especificada na cláusula FROM da consulta. Para obter mais informações, consulte [dicas de junção &#40; Transact-SQL &#41; ](../../t-sql/queries/hints-transact-sql-join.md).  
  
 Para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], aplicam essas dicas de junção para junções INNER em duas colunas incompatíveis de distribuição. Eles podem melhorar o desempenho da consulta, restringindo a quantidade de movimentação de dados que ocorre durante o processamento de consulta. Dicas de junção permitida para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] são da seguinte maneira:  
  
 REDUZIR  
 Reduz o número de linhas a ser movido para a tabela no lado direito da junção para tornar as duas tabelas de distribuição incompatível compatível. A dica REDUCE também é chamada de uma dica semijunção.  
  
 REPLICATE  
 Faz com que os valores na coluna de junção da tabela no lado esquerdo da junção devem ser replicadas para todos os nós. A tabela à direita é unida à versão dessas colunas replicada.  
  
 REDISTRIBUIR  
 Fontes de dados força dois deve ser distribuído em colunas especificadas na cláusula JOIN. Para uma tabela distribuída, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] executará uma movimentação de ordem aleatória. Para uma tabela replicada, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] executará uma movimentação de corte. Para entender esses tipos são movidos, consulte a seção "Operações de plano de consulta DMS" no tópico "Noções básicas sobre planos de consulta" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]. Essa dica pode melhorar o desempenho quando o plano de consulta está usando uma movimentação de difusão para resolver uma junção incompatível de distribuição.  
  
 JOIN  
 Indica que a operação de junção especificada deve acontecer entre as origens de tabela ou exibições especificadas.  
  
 ON \<search_condition>  
 Especifica o critério no qual a junção se baseia. Os critérios podem especificar qualquer predicado, embora colunas e operadores de comparação sejam frequentemente usados, por exemplo:  
  
```sql
SELECT p.ProductID, v.BusinessEntityID  
FROM Production.Product AS p   
JOIN Purchasing.ProductVendor AS v  
ON (p.ProductID = v.ProductID);  
  
```  
  
 Quando o critério especifica colunas, estas não precisam ter o mesmo nome ou o mesmo tipo de dados; no entanto, se os tipos de dados não forem iguais, eles deverão ser compatíveis ou tipos que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possa converter implicitamente. Se os tipos de dados não puderem ser convertidos implicitamente, o critério deverá converter o tipo de dados explicitamente usando a função CONVERT.  
  
 Poderá haver predicados que envolvam somente uma das tabelas unidas na cláusula ON. Tais predicados também podem estar na cláusula WHERE da consulta. Embora a presença de tais predicados não faça diferença para junções INNER, eles podem gerar um resultado diferente quando junções OUTER estão envolvidas. Isso ocorre porque os predicados na cláusula ON são aplicados à tabela antes da junção, ao passo que a cláusula WHERE é semanticamente aplicada ao resultado da junção.  
  
 Para obter mais informações sobre critérios de pesquisa e predicados, consulte [critério de pesquisa &#40; Transact-SQL &#41; ](../../t-sql/queries/search-condition-transact-sql.md).  
  
 CROSS JOIN  
 Especifica o produto cruzado de duas tabelas. Retorna as mesmas linhas como se nenhuma cláusula WHERE estivesse especificada em uma junção em estilo antigo que não seja SQL-92.  
  
 *left_table_source* {cruzada | Aplicar OUTER} *right_table_source*  
 Especifica que o *right_table_source* de aplicar o operador é avaliado em relação a cada linha do *left_table_source*. Essa funcionalidade é útil quando o *right_table_source* contém uma função com valor de tabela que usa valores de coluna a *left_table_source* como um de seus argumentos.  
  
 É necessário especificar CROSS ou OUTER com APPLY. Quando CROSS é especificado, nenhuma linha é criada quando o *right_table_source* é avaliado em relação uma linha especificada do *left_table_source* e retorna um conjunto de resultados vazio.  
  
 Quando OUTER é especificado, uma linha é produzida para cada linha do *left_table_source* mesmo quando o *right_table_source* é avaliado nessa linha e retorna um conjunto de resultados vazio.  
  
 Para obter mais informações, consulte a seção Comentários.  
  
 *left_table_source*  
 É uma origem de tabela conforme a definição no argumento anterior. Para obter mais informações, consulte a seção Comentários.  
  
 *right_table_source*  
 É uma origem de tabela conforme a definição no argumento anterior. Para obter mais informações, consulte a seção Comentários.  
  
 *table_source* PIVOT \<pivot_clause >  
 Especifica que o *table_source* se dinamize com base no *pivot_column*. *table_source* é uma tabela ou uma expressão de tabela. A saída é uma tabela que contém todas as colunas da *table_source* exceto o *pivot_column* e *value_column*. As colunas da *table_source*, exceto o *pivot_column* e *value_column*, são chamadas de colunas de agrupamento do operador pivot. Para obter mais informações sobre PIVOT e UNPIVOT, consulte [usando PIVOT e UNPIVOT](../../t-sql/queries/from-using-pivot-and-unpivot.md).  
  
 PIVOT executa uma operação de agrupamento na tabela de entrada em relação às colunas de agrupamento e retorna uma linha para cada grupo. Além disso, a saída contém uma coluna para cada valor especificado no *column_list* que aparece no *pivot_column* do *input_table*.  
  
 Para obter mais informações, consulte a seção Comentários a seguir.  
  
 *aggregate_function*  
 É um sistema ou uma função de agregação definida pelo usuário que aceita uma ou mais entradas. A função de agregação deve ser invariável para valores nulos. Uma função de agregação invariável para valores nulos não considera valores nulos no grupo enquanto está avaliando o valor de agregação.  
  
 A função de agregação de sistema COUNT (*) não é permitida.  
  
 *value_column*  
 É a coluna de valor do operador PIVOT. Quando usado com UNPIVOT, *value_column* não pode ser o nome de uma coluna existente na entrada *table_source*.  
  
 FOR *pivot_column*  
 É a coluna dinâmica do operador PIVOT. *pivot_column* deve ser de um tipo implicitamente ou explicitamente conversível em **nvarchar()**. Esta coluna não pode ser **imagem** ou **rowversion**.  
  
 Quando UNPIVOT é usado, *pivot_column* é o nome da coluna de saída que é restrita a partir de *table_source*. Não é possível haver uma coluna existente na *table_source* com esse nome.  
  
 IN (*column_list* )  
 Na cláusula PIVOT, lista os valores de *pivot_column* que se tornarão os nomes de coluna da tabela de saída. A lista não é possível especificar os nomes de coluna que já existem na entrada *table_source* que está sendo dinamizado.  
  
 Na cláusula UNPIVOT, lista as colunas na *table_source* que serão restritas em um único *pivot_column*.  
  
 *table_alias*  
 É o nome do alias da tabela de saída. *pivot_table_alias* deve ser especificado.  
  
 UNPIVOT \< unpivot_clause >  
 Especifica que a tabela de entrada é restrita de várias colunas em *column_list* em uma única coluna chamada *pivot_column*. Para obter mais informações sobre PIVOT e UNPIVOT, consulte [usando PIVOT e UNPIVOT](../../t-sql/queries/from-using-pivot-and-unpivot.md).  
  
 COMO de \<data_hora >  

**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  

  
 Retorna uma tabela com um único registro para cada linha que contém os valores que foram reais (atuais) no momento passado especificado. Internamente, uma união é executada entre a tabela temporal e sua tabela de histórico e os resultados são filtrados para retornar os valores na linha que era válida no ponto no tempo especificado o  *\<data_hora >* parâmetro. O valor de uma linha é considerado válido se o *system_start_time_column_name* valor é menor que ou igual ao  *\<data_hora >* o valor do parâmetro e o *system_end_time_ nome da coluna* valor é maior que o  *\<data_hora >* o valor do parâmetro.   
  
 DE \<data_hora_inicial > TO \<data_hora_final >

**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].

  
 Retorna uma tabela com os valores para todas as versões de registro que estavam ativas dentro do intervalo de tempo especificado, independentemente se eles começaram a ser ativos antes do  *\<data_hora_inicial >* valor de parâmetro para FROM argumento ou deixaram de ser ativos após o  *\<data_hora_final >* valor de parâmetro para o argumento TO. Internamente, uma união é executada entre a tabela temporal e sua tabela de histórico e os resultados são filtrados para retornar os valores para todas as versões de linha que estavam ativas a qualquer momento durante o intervalo de tempo especificado. Linhas que se tornaram ativas exatamente no limite inferior definido pelo ponto de extremidade FROM são incluídas e linhas que se tornaram ativas exatamente no limite superior definido pelo ponto de extremidade TO não são incluídas.  
  
 ENTRE \<data_hora_inicial > AND \<data_hora_final >  

**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Mesmo que acima no **FROM \<data_hora_inicial > TO \<data_hora_final >** descrição, exceto que ele inclui linhas que se tornaram ativas no limite superior definido pelo \<data_hora_final > ponto de extremidade.  
  
 CONTAINED IN (\<sdata_hora_inicial >, \<data_hora_final >)  

**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  

  
 Retorna uma tabela com os valores para todas as versões de registro que foram abertas e fechadas dentro do intervalo de tempo especificado definido por dois valores de data e hora para o argumento CONTAINED IN. As linhas que se tornaram ativas exatamente no limite inferior ou que deixaram de ser ativas exatamente no limite superior são incluídas.  
  
 ALL  
 Retorna uma tabela com os valores de todas as linhas da tabela atual e a tabela de histórico.  
  
## <a name="remarks"></a>Remarks  
 A cláusula FROM aceita a sintaxe SQL-92 para tabelas unidas e derivadas. Sintaxe SQL-92 fornece os operadores de junção INNER, LEFT OUTER, RIGHT OUTER, FULL OUTER e CROSS.  
  
 Há suporte para UNION e JOIN em uma cláusula FROM dentro de exibições e em tabelas derivadas e subconsultas.  
  
 Uma autojunção é uma tabela unida a ela mesma. As operações de inserção ou atualização que são baseadas em uma autojunção seguem a ordem da cláusula FROM.  
  
 Como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera as estatísticas de distribuição e cardinalidade de servidores vinculados que fornecem estatísticas de distribuição de coluna, a dica de junção REMOTE não é necessária para impor a avaliação de uma junção remotamente. O processador de consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera estatísticas remotas e determina se uma estratégia da junção remota é apropriada. A dica de junção REMOTE é útil para provedores que não fornecem estatísticas de distribuição de coluna.  
  
## <a name="using-apply"></a>Usando APPLY  
 Ambos os operandos à esquerda e à direita do operador APPLY são expressões de tabela. A principal diferença entre esses operandos é que o *right_table_source* pode usar uma função com valor de tabela que usa uma coluna a partir de *left_table_source* como um dos argumentos da função. O *left_table_source* pode incluir funções com valor de tabela, mas ele não pode conter argumentos que são colunas do *right_table_source*.  
  
 O operador APPLY funciona da seguinte maneira para criar a origem de tabela para a cláusula FROM:  
  
1.  Avalia *right_table_source* em cada linha do *left_table_source* para produzir conjuntos de linhas.  
  
     Os valores de *right_table_source* dependem *left_table_source*. *right_table_source* pode ser representado aproximadamente desta forma: `TVF(left_table_source.row)`, onde `TVF` é uma função com valor de tabela.  
  
2.  Combina os conjuntos de resultados que é produzidas para cada linha na avaliação de *right_table_source* com o *left_table_source* executando uma operação UNION ALL.  
  
     A lista de colunas produzida pelo resultado do operador APPLY é o conjunto de colunas do *left_table_source* combinado com a lista de colunas para o *right_table_source*.  
  
## <a name="using-pivot-and-unpivot"></a>Usando PIVOT e UNPIVOT  
 O *pivot_column* e *value_column* são colunas de agrupamento que são usadas pelo operador PIVOT. Este segue o seguinte processo para obter o conjunto de resultados de saída:  
  
1.  Executa um GROUP BY em seu *input_table* contra o agrupamento de colunas e produz uma linha de saída para cada grupo.  
  
     O agrupamento de colunas na linha de saída obter os valores de coluna correspondentes para esse grupo no *input_table*.  
  
2.  Gera valores para as colunas da lista de colunas para cada linha de saída da seguinte forma:  
  
    1.  Agrupando as linhas geradas em GROUP BY na etapa anterior em relação a *pivot_column*.  
  
         Para cada coluna de saída no *column_list*, selecionando um subgrupo que satisfaça a condição:  
  
         `pivot_column = CONVERT(<data type of pivot_column>, 'output_column')`  
  
    2.  *aggregate_function* é avaliado em relação a *value_column* nesse subgrupo e seu resultado é retornado como o valor correspondente *output_column*. Se o subgrupo estiver vazio, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gera um valor nulo para que *output_column*. Se a função de agregação for COUNT e o subgrupo estiver vazio, será retornado zero (0).  

> [!NOTE]
> Os identificadores de coluna no `UNPIVOT` cláusula siga o agrupamento de catálogo. Para [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], o agrupamento é sempre `SQL_Latin1_General_CP1_CI_AS`. Para [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] bancos de dados parcialmente independentes, o agrupamento é sempre `Latin1_General_100_CI_AS_KS_WS_SC`. Se a coluna for combinada com outras colunas e, em seguida, uma cláusula collate (`COLLATE DATABASE_DEFAULT`) é necessária para evitar conflitos.   
  
 Para obter mais informações sobre PIVOT e UNPIVOT, incluindo exemplos, consulte [usando PIVOT e UNPIVOT](../../t-sql/queries/from-using-pivot-and-unpivot.md).  
  
## <a name="permissions"></a>Permissões  
 Requer as permissões para a instrução DELETE, SELECT ou UPDATE.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-a-simple-from-clause"></a>A. Usando uma cláusula FROM simples  
 O exemplo a seguir recupera as colunas `TerritoryID` e `Name` da tabela `SalesTerritory` no banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql    
SELECT TerritoryID, Name  
FROM Sales.SalesTerritory  
ORDER BY TerritoryID ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
TerritoryID Name                            
----------- ------------------------------  
1           Northwest                       
2           Northeast                       
3           Central                         
4           Southwest                       
5           Southeast                       
6           Canada                          
7           France                          
8           Germany                         
9           Australia                       
10          United Kingdom                  
(10 row(s) affected)  
```  
  
### <a name="b-using-the-tablock-and-holdlock-optimizer-hints"></a>B. Usando as dicas de otimizador TABLOCK e HOLDLOCK  
 A transação parcial a seguir mostra como posicionar um bloqueio de tabela compartilhado explícito em `Employee` e como ler o índice. O bloqueio é mantido ao longo de toda a transação.  
  
```sql    
BEGIN TRAN  
SELECT COUNT(*)   
FROM HumanResources.Employee WITH (TABLOCK, HOLDLOCK) ;  
```  
  
### <a name="c-using-the-sql-92-cross-join-syntax"></a>C. Usando a sintaxe SQL-92 CROSS JOIN  
 O exemplo a seguir retorna o produto cruzado das tabelas `Employee` e `Department` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Uma lista de todas as combinações possíveis de `BusinessEntityID` linhas e todas as `Department` nome linhas são retornadas.  
  
```wql    
SELECT e.BusinessEntityID, d.Name AS Department  
FROM HumanResources.Employee AS e  
CROSS JOIN HumanResources.Department AS d  
ORDER BY e.BusinessEntityID, d.Name ;  
```  
  
### <a name="d-using-the-sql-92-full-outer-join-syntax"></a>D. Usando a sintaxe SQL-92 FULL OUTER JOIN  
 O exemplo a seguir retorna o nome do produto e quaisquer ordens de venda correspondentes na tabela `SalesOrderDetail` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Ele também retorna as ordens de venda que não têm produtos listados na tabela `Product`, bem como produtos com uma ordem de venda diferente daquela listada na tabela `Product`.  
  
```sql  
-- The OUTER keyword following the FULL keyword is optional.  
SELECT p.Name, sod.SalesOrderID  
FROM Production.Product AS p  
FULL OUTER JOIN Sales.SalesOrderDetail AS sod  
ON p.ProductID = sod.ProductID  
ORDER BY p.Name ;  
```  
  
### <a name="e-using-the-sql-92-left-outer-join-syntax"></a>E. Usando a sintaxe SQL-92 LEFT OUTER JOIN  
 O exemplo a seguir une duas tabelas em `ProductID` e preserva as linhas não correspondentes da tabela esquerda. É feita a correspondência da tabela `Product` com a tabela `SalesOrderDetail` nas colunas `ProductID` em cada tabela. Todos os produtos, ordenados ou não, aparecem no conjunto de resultados.  
  
```sql    
SELECT p.Name, sod.SalesOrderID  
FROM Production.Product AS p  
LEFT OUTER JOIN Sales.SalesOrderDetail AS sod  
ON p.ProductID = sod.ProductID  
ORDER BY p.Name ;  
```  
  
### <a name="f-using-the-sql-92-inner-join-syntax"></a>F. Usando a sintaxe SQL-92 INNER JOIN  
 O exemplo a seguir retorna todos os nomes de produtos e IDs de ordens de venda.  
  
```sql    
-- By default, SQL Server performs an INNER JOIN if only the JOIN   
-- keyword is specified.  
SELECT p.Name, sod.SalesOrderID  
FROM Production.Product AS p  
INNER JOIN Sales.SalesOrderDetail AS sod  
ON p.ProductID = sod.ProductID  
ORDER BY p.Name ;  
```  
  
### <a name="g-using-the-sql-92-right-outer-join-syntax"></a>G. Usando a sintaxe SQL-92 RIGHT OUTER JOIN  
 O exemplo a seguir une duas tabelas em `TerritoryID` e preserva as linhas não correspondentes da tabela direita. É feita a correspondência da tabela `SalesTerritory` com a tabela `SalesPerson` na coluna `TerritoryID` em cada tabela. Todos os vendedores aparecem no conjunto de resultados, tenham ou não um território atribuído.  
  
```sql    
SELECT st.Name AS Territory, sp.BusinessEntityID  
FROM Sales.SalesTerritory AS st   
RIGHT OUTER JOIN Sales.SalesPerson AS sp  
ON st.TerritoryID = sp.TerritoryID ;  
```  
  
### <a name="h-using-hash-and-merge-join-hints"></a>H. Usando dicas de junção HASH e MERGE  
 O exemplo a seguir executa uma junção de três tabelas entre as tabelas `Product`, `ProductVendor` e `Vendor` para criar uma lista de produtos e seus fornecedores. O otimizador de consulta une `Product` e `ProductVendor` (`p` e `pv`) usando uma junção MERGE. Em seguida, os resultados da junção MERGE de `Product` e `ProductVendor` (`p` e `pv`) são unidos por HASH à tabela `Vendor` para criar (`p` e `pv`) e `v`.  
  
> [!IMPORTANT]  
>  Após uma dica de junção ser especificada, a palavra-chave INNER não é mais opcional e deve ser explicitamente declarada para a execução de uma INNER JOIN.  
  
```sql    
SELECT p.Name AS ProductName, v.Name AS VendorName  
FROM Production.Product AS p   
INNER MERGE JOIN Purchasing.ProductVendor AS pv   
ON p.ProductID = pv.ProductID  
INNER HASH JOIN Purchasing.Vendor AS v  
ON pv.BusinessEntityID = v.BusinessEntityID  
ORDER BY p.Name, v.Name ;  
```  
  
### <a name="i-using-a-derived-table"></a>I. Usando uma tabela derivada  
 O exemplo a seguir usa uma tabela derivada, uma instrução `SELECT` após a clausula `FROM`, para retornar o nome e o sobrenome de todos os funcionários e as cidades em que moram.  
  
```sql    
SELECT RTRIM(p.FirstName) + ' ' + LTRIM(p.LastName) AS Name, d.City  
FROM Person.Person AS p  
INNER JOIN HumanResources.Employee e ON p.BusinessEntityID = e.BusinessEntityID   
INNER JOIN  
   (SELECT bea.BusinessEntityID, a.City   
    FROM Person.Address AS a  
    INNER JOIN Person.BusinessEntityAddress AS bea  
    ON a.AddressID = bea.AddressID) AS d  
ON p.BusinessEntityID = d.BusinessEntityID  
ORDER BY p.LastName, p.FirstName;  
```  
  
### <a name="j-using-tablesample-to-read-data-from-a-sample-of-rows-in-a-table"></a>J. Usando TABLESAMPLE para ler dados de uma amostra de linhas em uma tabela  
 O exemplo a seguir usa `TABLESAMPLE` na cláusula `FROM` para retornar aproximadamente `10` por cento de todas as linhas na tabela `Customer`.  
  
```sql    
SELECT *  
FROM Sales.Customer TABLESAMPLE SYSTEM (10 PERCENT) ;  
```  
  
### <a name="k-using-apply"></a>K. Usando APPLY  
 O seguinte exemplo presume que as tabelas com o esquema a seguir estão presentes no banco de dados:  
  
-   `Departments`: `DeptID`, `DivisionID`, `DeptName`, `DeptMgrID`  
  
-   `EmpMgr`: `MgrID`, `EmpID`  
  
-   `Employees`: `EmpID`, `EmpLastName`, `EmpFirstName`, `EmpSalary`  
  
 Há também uma função com valor de tabela, `GetReports(MgrID)` que retorna a lista de todos os funcionários (`EmpID`, `EmpLastName`, `EmpSalary`) subordinados direta ou indiretamente ao `MgrID` especificado.  
  
 O exemplo usa `APPLY` para retornar todos os departamentos e todos os funcionários do departamento. Se um departamento em particular não tiver funcionários, não haverá linhas retornadas para ele.  
  
```sql
SELECT DeptID, DeptName, DeptMgrID, EmpID, EmpLastName, EmpSalary  
FROM Departments d CROSS APPLY dbo.GetReports(d.DeptMgrID) ;  
```  
  
 Se desejar que a consulta gere linhas para os departamentos sem funcionários, o que irá gerar valores nulos para as colunas `EmpID`, `EmpLastName` e `EmpSalary`, use então `OUTER APPLY`.  
  
```sql
SELECT DeptID, DeptName, DeptMgrID, EmpID, EmpLastName, EmpSalary  
FROM Departments d OUTER APPLY dbo.GetReports(d.DeptMgrID) ;  
```  
  
### <a name="l-using-cross-apply"></a>L. Usando CROSS APPLY  
 O exemplo a seguir recupera um instantâneo de todos os planos de consulta residindo no cache de plano, consultando a exibição de gerenciamento dinâmico `sys.dm_exec_cached_plans` para recuperar os identificadores de plano de todas as consultas no cache. Em seguida, o operador `CROSS APPLY` é especificado para transmitir o identificador de plano a `sys.dm_exec_query_plan`. A saída de plano de execução XML de cada plano atualmente no cache de plano está na coluna `query_plan` da tabela retornada.  
  
```sql
USE master;  
GO  
SELECT dbid, object_id, query_plan   
FROM sys.dm_exec_cached_plans AS cp   
CROSS APPLY sys.dm_exec_query_plan(cp.plan_handle);   
GO  
```  
  
### <a name="m-using-for-systemtime"></a>M. Usando FOR SYSTEM_TIME  
  
**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 O exemplo a seguir usa o argumento de date_time_literal_or_variable FOR SYSTEM_TIME AS OF para retornar linhas da tabela que foram reais (atuais) a partir de 1 de janeiro de 2014.  
  
```sql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME AS OF '2014-01-01'  
WHERE ManagerID = 5;
```  
  
 O exemplo a seguir usa date_time_literal_or_variable FOR SYSTEM_TIME FROM date_time_literal_or_variable argumento para retornar todas as linhas que estavam ativas durante o período definido como começando com 1 de janeiro de 2013 e terminando com 1 de janeiro de 2014 excluindo o limite superior.  
  
```sql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME FROM '2013-01-01' TO '2014-01-01'  
WHERE ManagerID = 5;
```  
  
 O exemplo a seguir usa date_time_literal_or_variable para entre SYSTEM_TIME e date_time_literal_or_variable argumento para retornar todas as linhas que estavam ativas durante o período definido como começando com 1 de janeiro de 2013 e terminando com 1 de janeiro de 2014 incluindo o limite superior.  
  
```sql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME BETWEEN '2013-01-01' AND '2014-01-01'  
WHERE ManagerID = 5;
```  
  
 O exemplo a seguir usa o para argumento SYSTEM_TIME CONTAINED IN (date_time_literal_or_variable, date_time_literal_or_variable) para retornar todas as linhas que foram abertas e fechadas durante o período definido como começando com 1 de janeiro de 2013 e terminando com 1 de janeiro de 2014.  
  
```sql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME CONTAINED IN ( '2013-01-01', '2014-01-01' )  
WHERE ManagerID = 5;
```  
  
 O exemplo a seguir usa uma variável em vez de um literal para fornecer os valores de limite de data para a consulta.  
  
```sql
DECLARE @AsOfFrom datetime2 = dateadd(month,-12, sysutcdatetime());
DECLARE @AsOfTo datetime2 = dateadd(month,-6, sysutcdatetime());
  
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME FROM @AsOfFrom TO @AsOfTo  
WHERE ManagerID = 5;
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="n-using-the-inner-join-syntax"></a>N. Usando a sintaxe de junção interna  
 O exemplo a seguir retorna o `SalesOrderNumber`, `ProductKey`, e `EnglishProductName` colunas para o `FactInternetSales` e `DimProduct` tabelas onde a chave de junção, `ProductKey`, faz a correspondência em ambas as tabelas. O `SalesOrderNumber` e `EnglishProductName` colunas cada existem em uma das tabelas, portanto, não é necessário especificar o alias de tabela com essas colunas, conforme é mostrado; esses aliases são incluídos para facilitar a leitura. A palavra **AS** antes de um alias de nome não é obrigatório mas é recomendado para facilitar a leitura e estar de acordo com o padrão ANSI.  
  
```sql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
INNER JOIN DimProduct AS dp  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
 Desde o `INNER` palavra-chave não é necessária para junções internas, essa mesma consulta pode ser escrita como:  
  
```sql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
JOIN DimProduct AS dp  
ON dp.ProductKey = fis.ProductKey;  
```  
  
 Um `WHERE` cláusula também pode ser usada com essa consulta para limitar os resultados. Este exemplo limita os resultados para `SalesOrderNumber` valores maiores que 'SO5000':  
  
```sql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
JOIN DimProduct AS dp  
    ON dp.ProductKey = fis.ProductKey  
WHERE fis.SalesOrderNumber > 'SO50000'  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="o-using-the-left-outer-join-and-right-outer-join-syntax"></a>O. Usando a sintaxe LEFT OUTER JOIN e RIGHT OUTER JOIN  
 A exemplo a seguir adiciona o `FactInternetSales` e `DimProduct` tabelas no `ProductKey` colunas. A sintaxe de junção externa esquerda preserva as linhas não correspondentes da esquerda (`FactInternetSales`) tabela. Como o `FactInternetSales` tabela não contém nenhum `ProductKey` valores que não correspondem a `DimProduct` tabela, esta consulta retorna as mesmas linhas como o primeiro exemplo de junção interna acima.  
  
```sql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
LEFT OUTER JOIN DimProduct AS dp  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
 Essa consulta também poderia ser escrita sem a `OUTER` palavra-chave.  
  
 Em junções externas direitas, as linhas não correspondentes da tabela direita são preservadas. O exemplo a seguir retorna as mesmas linhas que o exemplo de junção externa esquerda acima.  
  
```sql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM DimProduct AS dp 
RIGHT OUTER JOIN FactInternetSales AS fis  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
 A consulta a seguir usa o `DimSalesTerritory` tabela como a tabela esquerda em uma junção externa esquerda. Recupera o `SalesOrderNumber` os valores do `FactInternetSales` tabela. Se não houver nenhuma ordem para um determinado `SalesTerritoryKey`, a consulta retornará um valor nulo para o `SalesOrderNumber` para aquela linha. Essa consulta é solicitada pelo `SalesOrderNumber` coluna, para que qualquer nulos nesta coluna aparecerá na parte superior dos resultados.  
  
```sql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
LEFT OUTER JOIN FactInternetSales AS fis  
    ON dst.SalesTerritoryKey = fis.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
 Essa consulta pode ser reescrita com uma junção externa direita para recuperar os mesmos resultados:  
  
```sql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM FactInternetSales AS fis 
RIGHT OUTER JOIN DimSalesTerritory AS dst  
    ON fis.SalesTerritoryKey = dst.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="p-using-the-full-outer-join-syntax"></a>P. Usando a sintaxe de junção externa completa  
 O exemplo a seguir demonstra uma junção externa completa, que retorna todas as linhas de ambas as tabelas unidas, mas retorna NULL para valores que não coincidem da outra tabela.  
  
```sql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
FULL OUTER JOIN FactInternetSales AS fis  
    ON dst.SalesTerritoryKey = fis.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
 Essa consulta também poderia ser escrita sem a `OUTER` palavra-chave.  
  
```sql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
FULL JOIN FactInternetSales AS fis  
    ON dst.SalesTerritoryKey = fis.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="q-using-the-cross-join-syntax"></a>Q. Usando a sintaxe CROSS JOIN  
 O exemplo a seguir retorna o produto cruzado do `FactInternetSales` e `DimSalesTerritory` tabelas. Uma lista de todas as combinações possíveis de `SalesOrderNumber` e `SalesTerritoryKey` são retornados. Observe a ausência de `ON` cláusula da consulta de junção cruzada.  
  
```sql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
CROSS JOIN FactInternetSales AS fis  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="r-using-a-derived-table"></a>R. Usando uma tabela derivada  
 O exemplo a seguir usa uma tabela derivada (um `SELECT` instrução após a `FROM` cláusula) para retornar o `CustomerKey` e `LastName` colunas de todos os clientes a `DimCustomer` de tabela com `BirthDate` valores posterior a 1º de janeiro de 1970 e o sobrenome 'Smith'.  
  
```sql
-- Uses AdventureWorks  
  
SELECT CustomerKey, LastName  
FROM  
   (SELECT * FROM DimCustomer  
    WHERE BirthDate > '01/01/1970') AS DimCustomerDerivedTable  
WHERE LastName = 'Smith'  
ORDER BY LastName;  
```  
  
### <a name="s-reduce-join-hint-example"></a>S. REDUZIR o exemplo de dica de junção  
 O exemplo a seguir usa o `REDUCE` dica de junção para alterar o processamento da tabela derivada dentro da consulta. Ao usar o `REDUCE` dica de junção nesta consulta, o `fis.ProductKey` é projetada, replicados e diferenciadas e, em seguida, associado ao `DimProduct` durante a ordem aleatória de `DimProduct` em `ProductKey`. A tabela derivada resultante é distribuída em `fis.ProductKey`.  
  
```sql
-- Uses AdventureWorks  
  
EXPLAIN SELECT SalesOrderNumber  
FROM  
   (SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
    FROM DimProduct AS dp   
      INNER REDUCE JOIN FactInternetSales AS fis   
          ON dp.ProductKey = fis.ProductKey  
   ) AS dTable  
ORDER BY SalesOrderNumber;  
```  
  
### <a name="t-replicate-join-hint-example"></a>T. Exemplo de dica de junção REPLICAR  
 O exemplo a seguir mostra a mesma consulta no exemplo anterior, exceto que um `REPLICATE` dica de junção é usada em vez do `REDUCE` dica de junção. Usar o `REPLICATE` dica faz com que os valores no `ProductKey` coluna (junção) do `FactInternetSales` tabela devem ser replicadas para todos os nós. O `DimProduct` tabela é unida à versão replicada desses valores.  
  
```sql
-- Uses AdventureWorks  
  
EXPLAIN SELECT SalesOrderNumber  
FROM  
   (SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
    FROM DimProduct AS dp   
      INNER REPLICATE JOIN FactInternetSales AS fis  
          ON dp.ProductKey = fis.ProductKey  
   ) AS dTable  
ORDER BY SalesOrderNumber;  
```  
  
### <a name="u-using-the-redistribute-hint-to-guarantee-a-shuffle-move-for-a-distribution-incompatible-join"></a>U. Usando a dica REDISTRIBUTE para garantir uma movimentação de ordem aleatória para uma junção incompatível de distribuição  
 A consulta a seguir usa a dica de consulta redistribuir em uma junção incompatível de distribuição. Isso garante que o otimizador de consulta usará uma movimentação de ordem aleatória no plano de consulta. Isso também garante que o plano de consulta não usará uma movimentação de transmissão que move uma tabela distribuída em uma tabela replicada.  
  
 No exemplo a seguir, a dica REDISTRIBUTE força uma movimentação de ordem aleatória na tabela FactInternetSales porque ProductKey é a coluna de distribuição de DimProduct e não é a coluna de distribuição para FactInternetSales.  
  
```sql
-- Uses AdventureWorks  
  
EXPLAIN  
SELECT dp.ProductKey, fis.SalesOrderNumber, fis.TotalProductCost  
FROM DimProduct AS dp 
INNER REDISTRIBUTE JOIN FactInternetSales AS fis  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
## <a name="see-also"></a>Consulte também  
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [INSERIR &#40;O Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENQUERY &#40;Transact-SQL&#41;](../../t-sql/functions/openquery-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
