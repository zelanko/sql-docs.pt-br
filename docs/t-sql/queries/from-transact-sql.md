---
title: FROM (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
dev_langs:
- TSQL
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
caps.latest.revision: 97
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: a1f0e63ad7df6755c49a536a2ae7249d3adf8d9d
ms.sourcegitcommit: 5e7f347b48b7d0400fb680645c28e781f2921141
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39496725"
---
# <a name="from-transact-sql"></a>FROM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Especifica as tabelas, exibições, tabelas derivadas e tabelas unidas usadas em instruções DELETE, SELECT e UPDATE no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Na instrução SELECT, a cláusula FROM é necessária, exceto quando a lista de seleção contém apenas constantes, variáveis e expressões aritméticas (sem nomes de coluna).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
    [<tablesample_clause>]  
    | derived_table [ AS ] table_alias [ ( column_alias [ ,...n ] ) ]  
    | <joined_table>  
}  
  
<tablesample_clause> ::=
    TABLESAMPLE ( sample_number [ PERCENT ] ) -- SQL Data Warehouse only  
 
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
>  O desempenho da consulta pode ser prejudicado com um grande número de tabelas referenciadas em uma consulta. O tempo de compilação e otimização também é afetado por outros fatores. Esses fatores incluem a presença de índices e exibições indexadas em cada \<table_source> e o tamanho de \<select_list> na instrução SELECT.  
  
 A ordem de origens de tabela após a palavra-chave FROM não afeta o conjunto de resultados que é retornado. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna erros quando aparecem nomes duplicados na cláusula FROM.  
  
 *table_or_view_name*  
 É o nome de uma tabela ou exibição.  
  
 Se a tabela ou exibição existir em outro banco de dados na mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use um nome totalmente qualificado no formato *database*.*schema*.*object_name*.  
  
 Se a tabela ou exibição existir fora da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use um nome de quatro partes no formato *linked_server*.*catalog*.*schema*.*object*. Para obter mais informações, consulte [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md). Um nome de quatro partes que é construído por meio da função [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) como a parte do servidor no nome também pode ser usado para especificar a origem da tabela remota. Quando OPENDATASOURCE é especificado, *database_name* e *schema_name* podem não se aplicar a todas as fontes de dados e podem estar sujeitos às funcionalidades do Provedor OLE DB que acessa o objeto remoto.  
  
 [AS] *table_alias*  
 É um alias para *table_source* que pode ser usado por conveniência ou para distinguir uma tabela ou exibição em uma autojunção ou subconsulta. Em geral, um alias é um nome de tabela abreviado usado para referência a colunas específicas das tabelas em uma junção. Se o nome da coluna existir em mais de uma tabela na junção, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exigirá que ele seja qualificado por um nome de tabela, nome de exibição ou alias. O nome da tabela não poderá ser usado se um alias estiver definido.  
  
 Quando uma tabela derivada, um conjunto de linhas, uma função com valor de tabela ou uma cláusula de operador (como PIVOT ou UNPIVOT) é usado, o *table_alias* obrigatório no final da cláusula é o nome da tabela associado para todas as colunas retornadas, incluindo colunas de agrupamento.  
  
 WITH (\<table_hint> )  
 Especifica que o otimizador de consulta use uma estratégia de otimização ou bloqueio com esta tabela e para esta instrução. Para obter mais informações, consulte [Dicas de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 *rowset_function*  

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  

  
 Especifica uma das funções de conjunto de linhas, como OPENROWSET, que retorna um objeto que pode ser usado no lugar de uma referência de tabela. Para obter mais informações sobre uma lista de funções de conjunto de linhas, consulte [Funções de conjunto de linhas &#40;Transact-SQL&#41;](../../t-sql/functions/rowset-functions-transact-sql.md).  
  
 O uso das funções OPENROWSET e OPENQUERY para especificar que um objeto remoto depende dos recursos do provedor OLE DB que acessa o objeto.  
  
 *bulk_column_alias*  

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  

  
 É um alias opcional para substituir um nome de coluna no conjunto de resultados. Os aliases de coluna são permitidos somente em instruções SELECT que usam a função OPENROWSET com a opção BULK. Ao usar *bulk_column_alias*, especifique um alias para cada coluna da tabela na mesma ordem que as colunas no arquivo.  
  
> [!NOTE]  
>  Este alias substitui o atributo NAME nos elementos COLUMN de um arquivo de formato XML, se houver.  
  
 *user_defined_function*  
 Especifica uma função com valor de tabela.  
  
 OPENXML \<openxml_clause>  

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  

  
 Fornece uma exibição de conjunto de linhas em um documento XML. Para obter mais informações, consulte [OPENXML &#40;SQL Server&#41;](../../t-sql/functions/openxml-transact-sql.md).  
  
 *derived_table*  
 É uma subconsulta que recupera linhas do banco de dados. *derived_table* é usada como entrada para a consulta externa.  
  
 *derived* *_table* pode usar o recurso do construtor de valor de tabela [!INCLUDE[tsql](../../includes/tsql-md.md)] para especificar várias linhas. Por exemplo, `SELECT * FROM (VALUES (1, 2), (3, 4), (5, 6), (7, 8), (9, 10) ) AS MyTable(a, b);`. Para obter mais informações, consulte [Construtor de valor de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/table-value-constructor-transact-sql.md).  
  
 *column_alias*  
 É um alias opcional para substituir um nome de coluna no conjunto de resultados da tabela derivada. Inclua um alias para cada coluna na lista de seleção e encerre a lista completa de aliases de coluna entre parênteses.  
  
 *table_or_view_name* FOR SYSTEM_TIME \<system_time>  

**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  

  
 Especifica que uma versão específica dos dados é retornada da tabela temporal especificada e sua tabela de histórico vinculada com controle de versão do sistema  
  
### <a name="tablesample-clause"></a>Cláusula Tablesample
**Aplica-se a:** SQL Server e Banco de Dados SQL 
 
 Especifica que uma amostra de dados da tabela é retornada. A amostra pode ser aproximada. Esta cláusula pode ser usada em qualquer tabela primária ou unida em uma instrução SELECT ou UPDATE. TABLESAMPLE não pode ser especificado com exibições.  
  
> [!NOTE]  
>  Quando você usa TABLESAMPLE em bancos de dados atualizados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o nível de compatibilidade do banco de dados é definido como 110 ou mais alto, PIVOT não é permitido em uma consulta CTE (expressão de tabela comum) recursiva. Para obter mais informações, veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
 SYSTEM  
 É um método de amostragem dependente de implementação especificado por padrões ISO. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esse é o único método de amostragem disponível e é aplicado por padrão. SYSTEM aplica um método de amostragem baseado em páginas em que um conjunto aleatório de páginas de uma tabela é escolhido para a amostra, e todas as linhas dessas páginas são retornadas como subconjunto da amostra.  
  
 *sample_number*  
 É uma expressão numérica constante exata ou aproximada que representa o percentual ou o número de linhas. Quando especificado com PERCENT, *sample_number* é convertido implicitamente em um valor **float**; caso contrário, é convertido em **bigint**. PERCENT é o padrão.  
  
 PERCENT  
 Especifica que um percentual *sample_number* das linhas da tabela deve ser recuperado da tabela. Quando PERCENT é especificado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna um valor aproximado do percentual especificado. Quando PERCENT é especificado, a expressão *sample_number* deve ser avaliada como um valor de 0 a 100.  
  
 ROWS  
 Especifica que, aproximadamente, *sample_number* de linhas será recuperado. Quando ROWS é especificado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna uma aproximação do número de linhas especificado. Quando ROWS é especificado, a expressão *sample_number* deve ser avaliada como um valor inteiro maior que zero.  
  
 REPEATABLE  
 Indica que a amostra selecionada pode ser retornada novamente. Quando for especificado com o mesmo valor de *repeat_seed*, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará o mesmo subconjunto de linhas, desde que não seja feita nenhuma alteração nas linhas da tabela. Quando for especificado com outro valor de *repeat_seed*, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provavelmente retornará uma amostra diferente das linhas da tabela. As seguintes ações na tabela são consideradas alterações: inserir, atualizar, excluir, recompilação do índice ou desfragmentação e restauração ou anexação do banco de dados.  
  
 *repeat_seed*  
 É uma expressão de inteiro constante usada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para gerar um número aleatório. *repeat_seed* é **bigint**. Se *repeat_seed* não for especificado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atribuirá um valor aleatório. Para um valor *repeat_seed* específico, o resultado da amostragem será sempre o mesmo se nenhuma alteração tiver sido aplicada à tabela. A expressão *repeat_seed* deve ser avaliada como um inteiro maior que zero.  
  
### <a name="tablesample-clause"></a>Cláusula Tablesample
**Aplica-se a:** SQL Data Warehouse

 Especifica que uma amostra de dados da tabela é retornada. A amostra pode ser aproximada. Esta cláusula pode ser usada em qualquer tabela primária ou unida em uma instrução SELECT ou UPDATE. TABLESAMPLE não pode ser especificado com exibições. 

 PERCENT  
 Especifica que um percentual *sample_number* das linhas da tabela deve ser recuperado da tabela. Quando PERCENT é especificado, o SQL Data Warehouse retorna um valor aproximado do percentual especificado. Quando PERCENT é especificado, a expressão *sample_number* precisa ser avaliada como um valor de 0 a 100.  


### <a name="joined-table"></a>Tabela unida 
Uma tabela unida é um conjunto de resultados que é o produto de duas ou mais tabelas. Para várias junções, use parênteses para alterar a ordem natural das junções.  
  
### <a name="join-type"></a>Tipo de junção
Especifica o tipo de operação de junção.  
  
 INNER  
 Especifica todos os pares de linhas correspondentes retornados. Descarta as linhas não correspondentes de ambas as tabelas. Quando nenhum tipo de junção é especificado, este é o padrão.  
  
 FULL [ OUTER ]  
 Especifica que uma linha da tabela esquerda ou direita que não atende à condição de junção seja incluída no conjunto de resultados, e as colunas de saída correspondentes à outra tabela sejam definidas como NULL. Isso ocorre além de todas as linhas normalmente retornadas por INNER JOIN.  
  
 LEFT [ OUTER ]  
 Especifica que todas as linhas da tabela esquerda que não atendem à condição de junção sejam incluídas no conjunto de resultados, e as colunas de saída da outra tabela sejam definidas como NULL além de todas as linhas retornadas pela junção interna.  
  
 RIGHT [OUTER]  
 Especifica que todas as linhas da tabela direita que não atendem à condição de junção sejam incluídas no conjunto de resultados, e as colunas de saída que correspondem à outra tabela sejam definidas como NULL, além de todas as linhas retornadas pela junção interna.  
  
### <a name="join-hint"></a>Dica de junção  
Para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDS](../../includes/sssds-md.md)], especifica que o otimizador de consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa uma dica de junção, ou um algoritmo de execução, por junção especificada na cláusula FROM da consulta. Para obter mais informações, consulte [Dicas de junção &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-join.md).  
  
 Para o [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], essas dicas de junção se aplicam a junções INNER em duas colunas incompatíveis com a distribuição. Elas podem melhorar o desempenho da consulta restringindo a quantidade de movimentação de dados que ocorre durante o processamento da consulta. As dicas de junção permitidas para o [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] são as seguintes:  
  
 REDUCE  
 Reduz o número de linhas a serem movidas para a tabela no lado direito da junção, a fim de tornar compatíveis as duas tabelas incompatíveis com a distribuição. A dica REDUCE também é chamada de uma dica de semijunção.  
  
 REPLICATE  
 Faz com que os valores na coluna de junção da tabela no lado esquerdo da junção sejam replicados para todos os nós. A tabela à direita é unida à versão replicada dessas colunas.  
  
 REDISTRIBUTE  
 Força duas fontes de dados a serem distribuídas nas colunas especificadas na cláusula JOIN. Para uma tabela distribuída, o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] executará uma movimentação de ordem aleatória. Para uma tabela replicada, o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] executará uma movimentação de corte. Para entender esses tipos de movimentação, consulte a seção "Operações de plano de consulta DMS" no tópico "Noções básicas sobre planos de consulta" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]. Essa dica pode melhorar o desempenho quando o plano de consulta usa uma movimentação de difusão para resolver uma junção incompatível com a distribuição.  
  
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
  
 Para obter mais informações sobre critérios de pesquisa e predicados, consulte [Critério de pesquisa &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
 CROSS JOIN  
 Especifica o produto cruzado de duas tabelas. Retorna as mesmas linhas como se nenhuma cláusula WHERE estivesse especificada em uma junção em estilo antigo que não seja SQL-92.  
  
 *left_table_source* { CROSS | OUTER } APPLY *right_table_source*  
 Especifica que a *right_table_source* do operador APPLY é avaliada em cada linha da *left_table_source*. Essa funcionalidade é útil quando a *right_table_source* contém uma função com valor de tabela que usa valores de coluna da *left_table_source* como um de seus argumentos.  
  
 É necessário especificar CROSS ou OUTER com APPLY. Quando CROSS é especificado, nenhuma linha é produzida quando a *right_table_source* é avaliada em uma linha especificada da *left_table_source* e retorna um conjunto de resultados vazio.  
  
 Quando OUTER é especificado, uma linha é produzida para cada linha da *left_table_source*, mesmo quando a *right_table_source* é avaliada nessa linha e retorna um conjunto de resultados vazio.  
  
 Para obter mais informações, consulte a seção Comentários.  
  
 *left_table_source*  
 É uma origem de tabela conforme a definição no argumento anterior. Para obter mais informações, consulte a seção Comentários.  
  
 *right_table_source*  
 É uma origem de tabela conforme a definição no argumento anterior. Para obter mais informações, consulte a seção Comentários.  
  
### <a name="pivot-clause"></a>Cláusula PIVOT

 *table_source* PIVOT \<pivot_clause>  
 Especifica que a *table_source* é dinamizada com base na *pivot_column*. *table_source* é uma tabela ou uma expressão de tabela. A saída é uma tabela que contém todas as colunas da *table_source*, exceto a *pivot_column* e *value_column*. As colunas da *table_source*, exceto a *pivot_column* e a *value_column*, são chamadas as colunas de agrupamento do operador original. Para obter mais informações sobre PIVOT e UNPIVOT, consulte [Usando PIVOT e UNPIVOT](../../t-sql/queries/from-using-pivot-and-unpivot.md).  
  
 PIVOT executa uma operação de agrupamento na tabela de entrada em relação às colunas de agrupamento e retorna uma linha para cada grupo. Além disso, a saída contém uma coluna para cada valor especificado na *column_list* exibido na *pivot_column* da *input_table*.  
  
 Para obter mais informações, consulte a seção Comentários a seguir.  
  
 *aggregate_function*  
 É um sistema ou uma função de agregação definida pelo usuário que aceita uma ou mais entradas. A função de agregação deve ser invariável para valores nulos. Uma função de agregação invariável para valores nulos não considera valores nulos no grupo enquanto está avaliando o valor de agregação.  
  
 A função de agregação de sistema COUNT (*) não é permitida.  
  
 *value_column*  
 É a coluna de valor do operador PIVOT. Quando usado com UNPIVOT, *value_column* não pode ser o nome de uma coluna existente na *table_source* de entrada.  
  
 FOR *pivot_column*  
 É a coluna dinâmica do operador PIVOT. *pivot_column* deve ser de um tipo implícita ou explicitamente conversível em **nvarchar()**. Esta coluna não pode ser **image** ou **rowversion**.  
  
 Quando UNPIVOT é usado, *pivot_column* é o nome da coluna de saída que é reduzida com base na *table_source*. Não pode haver uma coluna em *table_source* com esse nome.  
  
 IN (*column_list* )  
 Na cláusula PIVOT, lista os valores na *pivot_column* que se tornarão os nomes de coluna da tabela de saída. A lista não pode especificar nomes de coluna já existentes na *table_source* de entrada que está sendo dinamizada.  
  
 Na cláusula UNPIVOT, lista as colunas na *table_source* que serão reduzidas a uma única *pivot_column*.  
  
 *table_alias*  
 É o nome do alias da tabela de saída. *pivot_table_alias* deve ser especificado.  
  
 UNPIVOT \<unpivot_clause>  
 Especifica que a tabela de entrada é reduzida com base em várias colunas na *column_list* a uma única coluna chamada *pivot_column*. Para obter mais informações sobre PIVOT e UNPIVOT, consulte [Usando PIVOT e UNPIVOT](../../t-sql/queries/from-using-pivot-and-unpivot.md).  
  
 AS OF \<date_time>  

**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  

  
 Retorna uma tabela com um único registro para cada linha que contém os valores que foram reais (atuais) no momento passado especificado. Internamente, uma união é executada entre a tabela temporal e sua tabela de histórico e os resultados são filtrados para retornar os valores na linha que era válida no ponto no tempo especificado pelo parâmetro *\<date_time>*. O valor de uma linha é considerado válido se o valor de *system_start_time_column_name* é menor ou igual ao valor do parâmetro *\<date_time>* e o valor de *system_end_time_column_name* é maior que o valor do parâmetro *\<date_time>*.   
  
 FROM \<start_date_time> TO \<end_date_time>

**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].

  
 Retorna uma tabela com os valores para todas as versões de registro que estavam ativas no intervalo de tempo especificado, sem levar em conta se eles começaram a estar ativos antes do valor de parâmetro *\<start_date_time>* para o argumento FROM ou deixaram de estar ativos após o valor de parâmetro *\<end_date_time>* para o argumento TO. Internamente, uma união é executada entre a tabela temporal e sua tabela de histórico e os resultados são filtrados para retornar os valores para todas as versões de linha que estavam ativas a qualquer momento durante o intervalo de tempo especificado. As linhas que se tornaram ativas exatamente no limite inferior definido pelo ponto de extremidade FROM são incluídas e as linhas que se tornaram ativas exatamente no limite superior definido pelo ponto de extremidade TO não são incluídas.  
  
 BETWEEN \<start_date_time> AND \<end_date_time>  

**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 A mesma descrição acima para **FROM \<start_date_time> TO \<end_date_time>** é válida, exceto que ela inclui linhas que se tornaram ativas no limite superior definido pelo ponto de extremidade \<end_date_time>.  
  
 CONTAINED IN (\<start_date_time>, \<end_date_time>)  

**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  

  
 Retorna uma tabela com os valores para todas as versões de registro que foram abertas e fechadas dentro do intervalo de tempo especificado definido por dois valores de data e hora para o argumento CONTAINED IN. As linhas que se tornaram ativas exatamente no limite inferior ou que deixaram de ser ativas exatamente no limite superior são incluídas.  
  
 ALL  
 Retorna uma tabela com os valores de todas as linhas da tabela atual e da tabela de histórico.  
  
## <a name="remarks"></a>Remarks  
 A cláusula FROM aceita a sintaxe SQL-92 para tabelas unidas e derivadas. Sintaxe SQL-92 fornece os operadores de junção INNER, LEFT OUTER, RIGHT OUTER, FULL OUTER e CROSS.  
  
 Há suporte para UNION e JOIN em uma cláusula FROM dentro de exibições e em tabelas derivadas e subconsultas.  
  
 Uma autojunção é uma tabela unida a ela mesma. As operações de inserção ou atualização que são baseadas em uma autojunção seguem a ordem da cláusula FROM.  
  
 Como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera as estatísticas de distribuição e cardinalidade de servidores vinculados que fornecem estatísticas de distribuição de coluna, a dica de junção REMOTE não é necessária para impor a avaliação de uma junção remotamente. O processador de consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera estatísticas remotas e determina se uma estratégia da junção remota é apropriada. A dica de junção REMOTE é útil para provedores que não fornecem estatísticas de distribuição de coluna.  
  
## <a name="using-apply"></a>Usando APPLY  
 Ambos os operandos à esquerda e à direita do operador APPLY são expressões de tabela. A principal diferença entre esses operandos é que *right_table_source* pode usar uma função com valor de tabela que usa uma coluna da *left_table_source* como um dos argumentos da função. A *left_table_source* pode incluir funções com valor de tabela, mas não pode conter argumentos que são colunas da *right_table_source*.  
  
 O operador APPLY funciona da seguinte maneira para criar a origem de tabela para a cláusula FROM:  
  
1.  Avalia *right_table_source* em cada linha da *left_table_source* para produzir conjuntos de linhas.  
  
     Os valores na *right_table_source* dependem de *left_table_source*. *right_table_source* pode ser representada aproximadamente da seguinte maneira: `TVF(left_table_source.row)`, em que `TVF` é uma função com valor de tabela.  
  
2.  Combina os conjuntos de resultados que são produzidos para cada linha na avaliação de *right_table_source* com a *left_table_source* executando uma operação UNION ALL.  
  
     A lista de colunas produzida pelo resultado do operador APPLY é o conjunto de colunas da *left_table_source* combinado à lista de colunas da *right_table_source*.  
  
## <a name="using-pivot-and-unpivot"></a>Usando PIVOT e UNPIVOT  
 A *pivot_column* e a *value_column* são colunas de agrupamento usadas pelo operador PIVOT. Este segue o seguinte processo para obter o conjunto de resultados de saída:  
  
1.  Executa um GROUP BY em sua *input_table* nas colunas de agrupamento e produz uma linha de saída para cada grupo.  
  
     As colunas de agrupamento na linha de saída obtêm os valores de coluna correspondentes para o grupo na *input_table*.  
  
2.  Gera valores para as colunas da lista de colunas para cada linha de saída da seguinte forma:  
  
    1.  Agrupando ainda as linhas geradas em GROUP BY na etapa anterior na *pivot_column*.  
  
         Para cada coluna de saída na *column_list*, selecionando um subgrupo que atenda à condição:  
  
         `pivot_column = CONVERT(<data type of pivot_column>, 'output_column')`  
  
    2.  *aggregate_function* é avaliada na *value_column* desse subgrupo e seu resultado é retornado como o valor da *output_column* correspondente. Se o subgrupo estiver vazio, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerará um valor nulo para essa *output_column*. Se a função de agregação for COUNT e o subgrupo estiver vazio, será retornado zero (0).  

> [!NOTE]
> Os identificadores de coluna na cláusula `UNPIVOT` seguem o agrupamento de catálogo. Para o [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], o agrupamento é sempre `SQL_Latin1_General_CP1_CI_AS`. Para bancos de dados parcialmente independentes do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], o agrupamento é sempre `Latin1_General_100_CI_AS_KS_WS_SC`. Se a coluna for combinada com outras colunas, uma cláusula COLLATE (`COLLATE DATABASE_DEFAULT`) será necessária para evitar conflitos.   
  
 Para obter mais informações sobre PIVOT e UNPIVOT, incluindo exemplos, consulte [Usando PIVOT e UNPIVOT](../../t-sql/queries/from-using-pivot-and-unpivot.md).  
  
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
 O exemplo a seguir retorna o produto cruzado das tabelas `Employee` e `Department` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Uma lista de todas as possíveis combinações de linhas de `BusinessEntityID` e todas as linhas de nome de `Department` é retornada.  
  
```sql    
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
  
**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 O exemplo a seguir usa o argumento FOR SYSTEM_TIME AS OF date_time_literal_or_variable para retornar linhas da tabela que eram reais (atuais) a partir de 1º de janeiro de 2014.  
  
```sql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME AS OF '2014-01-01'  
WHERE ManagerID = 5;
```  
  
 O exemplo a seguir usa o argumento FOR SYSTEM_TIME FROM date_time_literal_or_variable TO date_time_literal_or_variable para retornar todas as linhas que estavam ativas durante o período definido começando em 1º de janeiro de 2013 e terminando em 1º de janeiro de 2014, excluindo o limite superior.  
  
```sql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME FROM '2013-01-01' TO '2014-01-01'  
WHERE ManagerID = 5;
```  
  
 O exemplo a seguir usa o argumento FOR SYSTEM_TIME BETWEEN date_time_literal_or_variable AND date_time_literal_or_variable para retornar todas as linhas que estavam ativas durante o período definido começando em 1º de janeiro de 2013 e terminando em 1º de janeiro de 2014, incluindo o limite superior.  
  
```sql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME BETWEEN '2013-01-01' AND '2014-01-01'  
WHERE ManagerID = 5;
```  
  
 O exemplo a seguir usa o argumento FOR SYSTEM_TIME CONTAINED IN (date_time_literal_or_variable, date_time_literal_or_variable) para retornar todas as linhas que estavam abertas e fechadas durante o período definido começando em 1º de janeiro de 2013 e terminando em 1º de janeiro de 2014.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="n-using-the-inner-join-syntax"></a>N. Usando a sintaxe de INNER JOIN  
 O exemplo a seguir retorna as colunas `SalesOrderNumber`, `ProductKey` e `EnglishProductName` das tabelas `FactInternetSales` e `DimProduct`, em que a chave de junção, `ProductKey`, é correspondente em ambas as tabelas. As colunas `SalesOrderNumber` e `EnglishProductName` existem em uma das tabelas e, portanto, não é necessário especificar o alias da tabela com essas colunas, conforme mostrado; esses aliases são incluídos para facilitar a leitura. A palavra **AS** antes de um alias de nome não é obrigatória, mas é recomendada para facilitar a leitura e estar em conformidade com o padrão ANSI.  
  
```sql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
INNER JOIN DimProduct AS dp  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
 Como a palavra-chave `INNER` não é obrigatória para junções internas, essa mesma consulta pode ser escrita como:  
  
```sql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
JOIN DimProduct AS dp  
ON dp.ProductKey = fis.ProductKey;  
```  
  
 Uma cláusula `WHERE` também pode ser usada com essa consulta para limitar os resultados. Este exemplo limita os resultados a valores `SalesOrderNumber` maiores que 'SO5000':  
  
```sql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
JOIN DimProduct AS dp  
    ON dp.ProductKey = fis.ProductKey  
WHERE fis.SalesOrderNumber > 'SO50000'  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="o-using-the-left-outer-join-and-right-outer-join-syntax"></a>O. Usando a sintaxe de LEFT OUTER JOIN e RIGHT OUTER JOIN  
 O exemplo a seguir une as tabelas `FactInternetSales` e `DimProduct` nas colunas `ProductKey`. A sintaxe da junção externa esquerda preserva as linhas não correspondentes da tabela à esquerda (`FactInternetSales`). Como a tabela `FactInternetSales` não contém nenhum valor `ProductKey` não correspondente na tabela `DimProduct`, essa consulta retorna as mesmas linhas como o primeiro exemplo de junção interna acima.  
  
```sql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
LEFT OUTER JOIN DimProduct AS dp  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
 Essa consulta também pode ser escrita sem a palavra-chave `OUTER`.  
  
 Em junções externas direitas, as linhas não correspondentes da tabela à direita são preservadas. O exemplo a seguir retorna as mesmas linhas que o exemplo de junção externa esquerda acima.  
  
```sql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM DimProduct AS dp 
RIGHT OUTER JOIN FactInternetSales AS fis  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
 A consulta a seguir usa a tabela `DimSalesTerritory` como a tabela à esquerda em uma junção externa esquerda. Recupera os valores `SalesOrderNumber` da tabela `FactInternetSales`. Se não houver nenhuma ordem para determinada `SalesTerritoryKey`, a consulta retornará um valor NULL para o `SalesOrderNumber` nessa linha. Essa consulta é ordenada pela coluna `SalesOrderNumber`, de modo que os valores NULL dessa coluna serão exibidos na parte superior dos resultados.  
  
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
  
### <a name="p-using-the-full-outer-join-syntax"></a>P. Usando a sintaxe de FULL OUTER JOIN  
 O exemplo a seguir demonstra uma junção externa completa, que retorna todas as linhas de ambas as tabelas unidas, mas retorna NULL para valores não correspondentes da outra tabela.  
  
```sql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
FULL OUTER JOIN FactInternetSales AS fis  
    ON dst.SalesTerritoryKey = fis.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
 Essa consulta também pode ser escrita sem a palavra-chave `OUTER`.  
  
```sql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
FULL JOIN FactInternetSales AS fis  
    ON dst.SalesTerritoryKey = fis.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="q-using-the-cross-join-syntax"></a>Q. Usando a sintaxe de CROSS JOIN  
 O exemplo a seguir retorna o produto cruzado das tabelas `FactInternetSales` e `DimSalesTerritory`. Uma lista de todas as combinações possíveis de `SalesOrderNumber` e `SalesTerritoryKey` é retornada. Observe a ausência da cláusula `ON` da consulta de união cruzada.  
  
```sql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
CROSS JOIN FactInternetSales AS fis  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="r-using-a-derived-table"></a>R. Usando uma tabela derivada  
 O exemplo a seguir usa uma tabela derivada (uma instrução `SELECT` após a cláusula `FROM`) para retornar as colunas `CustomerKey` e `LastName` de todos os clientes na tabela `DimCustomer` com valores `BirthDate` posteriores a 1º de janeiro de 1970 e o sobrenome 'Fernandes'.  
  
```sql
-- Uses AdventureWorks  
  
SELECT CustomerKey, LastName  
FROM  
   (SELECT * FROM DimCustomer  
    WHERE BirthDate > '01/01/1970') AS DimCustomerDerivedTable  
WHERE LastName = 'Smith'  
ORDER BY LastName;  
```  
  
### <a name="s-reduce-join-hint-example"></a>S. Exemplo de dica de junção de REDUCE  
 O exemplo a seguir usa a dica de junção `REDUCE` para alterar o processamento da tabela derivada dentro da consulta. Ao usar a dica de junção `REDUCE` nesta consulta, a `fis.ProductKey` é projetada, replicada e diferenciada e, em seguida, unida ao `DimProduct` durante a ordem aleatória de `DimProduct` no `ProductKey`. A tabela derivada resultante é distribuída em `fis.ProductKey`.  
  
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
  
### <a name="t-replicate-join-hint-example"></a>T. Exemplo de dica de junção de REPLICATE  
 Este próximo exemplo mostra a mesma consulta como no exemplo anterior, exceto que uma dica de junção `REPLICATE` é usada, em vez da dica de junção `REDUCE`. O uso da dica `REPLICATE` faz com que os valores na coluna `ProductKey` (de junção) da tabela `FactInternetSales` sejam replicados para todos os nós. A tabela `DimProduct` é unida à versão replicada desses valores.  
  
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
  
### <a name="u-using-the-redistribute-hint-to-guarantee-a-shuffle-move-for-a-distribution-incompatible-join"></a>U. Usando a dica REDISTRIBUTE para assegurar uma movimentação de Ordem Aleatória para uma junção incompatível com a distribuição  
 A consulta a seguir usa a dica de consulta REDISTRIBUTE em uma junção incompatível com a distribuição. Isso garante que o otimizador de consulta usará uma movimentação de Ordem Aleatória no plano de consulta. Isso também garante que o plano de consulta não usará uma movimentação de Difusão que move uma tabela distribuída para uma tabela replicada.  
  
 No exemplo a seguir, a dica REDISTRIBUTE força uma movimentação de Ordem Aleatória na tabela FactInternetSales porque ProductKey é a coluna de distribuição de DimProduct e não é a coluna de distribuição para FactInternetSales.  
  
```sql
-- Uses AdventureWorks  
  
EXPLAIN  
SELECT dp.ProductKey, fis.SalesOrderNumber, fis.TotalProductCost  
FROM DimProduct AS dp 
INNER REDISTRIBUTE JOIN FactInternetSales AS fis  
    ON dp.ProductKey = fis.ProductKey;  
```  

### <a name="v-using-tablesample-to-read-data-from-a-sample-of-rows-in-a-table"></a>V. Usando TABLESAMPLE para ler dados de uma amostra de linhas em uma tabela  
 O exemplo a seguir usa `TABLESAMPLE` na cláusula `FROM` para retornar aproximadamente `10` por cento de todas as linhas na tabela `Customer`.  
  
```sql    
SELECT *  
FROM Sales.Customer TABLESAMPLE SYSTEM (10 PERCENT) ;
```
  
## <a name="see-also"></a>Consulte Também  
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENQUERY &#40;Transact-SQL&#41;](../../t-sql/functions/openquery-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
