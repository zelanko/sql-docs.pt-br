---
title: MERGE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- MERGE
- MERGE_TSQL
dev_langs: TSQL
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
caps.latest.revision: "76"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: dd8ecb3609dd70516023afe84125252c708ad1ad
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="merge-transact-sql"></a>MERGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Realiza operações de inserção, atualização ou exclusão em uma tabela de destino com base nos resultados da junção com a tabela de origem. Por exemplo, você pode sincronizar duas tabelas inserindo, atualizando ou excluindo linhas em uma tabela com base nas diferenças encontradas na outra tabela.  
  
 **Dica de desempenho:** o comportamento condicional descrito para a instrução MERGE funciona melhor quando as duas tabelas têm uma mistura complexa de características de correspondência. Por exemplo, inserindo uma linha se ela não existir, ou atualizando a linha se ela corresponder. Ao simplesmente atualizar uma tabela com base nas linhas de outra tabela, desempenho e escalabilidade aprimorados podem ser obtidos com as instruções INSERT, UPDATE e DELETE básicas. Por exemplo:  
  
```  
INSERT tbl_A (col, col2)  
SELECT col, col2   
FROM tbl_B   
WHERE NOT EXISTS (SELECT col FROM tbl_A A2 WHERE A2.col = tbl_B.col);  
```  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
    { [ NOT ] <predicate> | ( <search_condition> ) }   
    [ { AND | OR } [ NOT ] { <predicate> | ( <search_condition> ) } ]   
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
 COM \<common_table_expression >  
 Especifica a exibição ou o conjunto de resultados nomeado temporário, também conhecido como expressão de tabela comum, definido no escopo da instrução MERGE. O conjunto de resultados é derivado de uma consulta simples e referenciado pela instrução MERGE. Para obter mais informações, consulte [com common_table_expression &#40; Transact-SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 Parte superior ( *expressão* ) [%]  
 Especifica o número ou a porcentagem de linhas afetadas. *expressão* pode ser um número ou uma porcentagem das linhas. As linhas referenciadas na expressão TOP não são organizadas em nenhuma ordem. Para obter mais informações, consulte [TOP &#40; Transact-SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
  
 A cláusula TOP é aplicada depois que toda a tabela de origem e toda a tabela de destino são unidas e as linhas unidas que não se qualificam para uma ação de inserção, atualização ou exclusão são removidas. A cláusula TOP ainda reduz o número de linhas unidas para o valor especificado e as ações de inserção, atualização ou exclusão são aplicadas às linhas unidas restantes de uma forma não ordenada. Ou seja, não há nenhuma ordem na qual as linhas são distribuídas entre as ações definidas nas cláusulas WHEN. Por exemplo, especificar TOP (10) afeta dez linhas. Dessas linhas, sete podem ser atualizadas e três inseridas, ou uma pode ser excluída, cinco atualizadas e quatro inseridas etc.  
  
 Como a instrução MERGE executa um exame completo das tabelas de origem e de destino, o desempenho de E/S pode ser afetado ao usar a cláusula TOP para modificar uma tabela grande criando vários lotes. Neste cenário, é importante garantir que todos os lotes sucessivos se destinem a novas linhas.  
  
 *database_name*  
 É o nome do banco de dados no qual *target_table* está localizado.  
  
 *schema_name*  
 É o nome do esquema ao qual *target_table* pertence.  
  
 *target_table*  
 É a tabela ou exibição na qual os dados de linhas a partir de \<table_source > são correspondidas com base em \<clause_search_condition >. *target_table* é o destino de qualquer inserção, atualização ou operações de exclusão especificadas pelas cláusulas WHEN da instrução MERGE.  
  
 Se *target_table* é uma exibição, as ações em relação a ela devem atender às condições para atualizar exibições. Para obter mais informações, consulte [modificar dados por meio de um modo de exibição](../../relational-databases/views/modify-data-through-a-view.md).  
  
 *target_table* não pode ser uma tabela remota. *target_table* não pode ter nenhuma regra definida nela.  
  
 [COMO] *table_alias*  
 É um nome alternativo usado para fazer referência a uma tabela.  
  
 USANDO \<table_source >  
 Especifica a fonte de dados que está de acordo com as linhas de dados *target_table* com base em \<merge_search condition >. O resultado dessa correspondência dita as ações a serem tomadas pelas cláusulas WHEN da instrução MERGE. \<table_source > pode ser uma tabela remota ou uma tabela derivada que acessa tabelas remotas. 
  
 \<table_source > pode ser uma tabela derivada que usa o [!INCLUDE[tsql](../../includes/tsql-md.md)] [construtor de valor de tabela](../../t-sql/queries/table-value-constructor-transact-sql.md) para construir uma tabela especificando várias linhas.  
  
 Para obter mais informações sobre a sintaxe e os argumentos dessa cláusula, consulte [FROM &#40; Transact-SQL &#41; ](../../t-sql/queries/from-transact-sql.md).  
  
 ON \<merge_search_condition >  
 Especifica as condições em que \<table_source > é Unido *target_table* para determinar onde elas correspondem. 
  
> [!CAUTION]  
>  É importante especificar apenas as colunas da tabela de destino que são usadas para fins de correspondência. Ou seja, especifique as colunas da tabela de destino que são comparadas à coluna correspondente da tabela de origem. Não tente melhorar o desempenho de uma consulta filtrando linhas na tabela de destino na cláusula ON, por exemplo, especificando `AND NOT target_table.column_x = value`. Isso pode retornar resultados inesperados e incorretos.  
  
 Quando a correspondência, em seguida, \<merge_matched >  
 Especifica que todas as linhas de *target_table* que correspondem às linhas retornadas por \<table_source > ON \<merge_search_condition > e atendem a qualquer critério de pesquisa adicionais, são atualizadas ou excluídas de acordo com o \<merge_matched > cláusula.  
  
 A instrução MERGE pode ter no máximo duas cláusulas WHEN MATCHED. Se duas cláusulas forem especificadas, a primeira cláusula deve ser acompanhada por um AND \<search_condition > cláusula. Para qualquer linha especificada, a segunda cláusula WHEN MATCHED será aplicada somente se a primeira não for. Se houver duas cláusulas WHEN MATCHED, uma delas deverá especificar uma ação UPDATE e a outra, uma ação DELETE. Se UPDATE for especificada no \<merge_matched > cláusula e mais de uma linha de \<table_source > corresponder a uma linha em *target_table* com base em \<merge_search_condition >, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]retornará um erro. A instrução MERGE não pode atualizar a mesma linha mais de uma vez, nem atualizar e excluir a mesma linha.  
  
 Quando não correspondem às [destino], em seguida, \<merge_not_matched >  
 Especifica que uma linha é inserida na *target_table* para cada linha retornada por \<table_source > ON \<merge_search_condition > que não corresponde a uma linha em *target_table*, mas atende a uma condição de pesquisa adicionais, se presente. Para inserir os valores são especificados pelo \<merge_not_matched > cláusula. A instrução MERGE pode ter apenas uma cláusula WHEN NOT MATCHED.  
  
 Quando NOT MATCHED BY SOURCE, em seguida, \<merge_matched >  
 Especifica que todas as linhas de *target_table* que não correspondem às linhas retornadas por \<table_source > ON \<merge_search_condition >, e que atendem a qualquer critério de pesquisa adicionais, o é atualizado ou excluídas de acordo com o \<merge_matched > cláusula.  
  
 A instrução MERGE pode ter, no máximo, duas cláusulas WHEN NOT MATCHED BY SOURCE. Se duas cláusulas forem especificadas, a primeira cláusula deve ser acompanhada por um AND \<clause_search_condition > cláusula. Para qualquer linha especificada, a segunda cláusula WHEN NOT MATCHED BY SOURCE será aplicada somente se a primeira não for. Se houver duas cláusulas WHEN NOT MATCHED BY SOURCE, uma delas deverá especificar uma ação UPDATE e a outra, uma ação DELETE. Somente as colunas da tabela de destino podem ser referenciadas na \<clause_search_condition >.  
  
 Quando nenhuma linha será retornada por \<table_source >, colunas na tabela de origem não podem ser acessadas. Se a ação update ou delete especificada no \<merge_matched > cláusula faz referência a colunas na tabela de origem, o erro 207 (nome de coluna inválido) será retornado. Por exemplo, a cláusula `WHEN NOT MATCHED BY SOURCE THEN UPDATE SET TargetTable.Col1 = SourceTable.Col1` pode fazer a instrução falhar porque não é possível acessar `Col1` na tabela de origem.  
  
 E \<clause_search_condition >  
 Especifica qualquer critério de pesquisa válido. Para obter mais informações, consulte [critério de pesquisa &#40; Transact-SQL &#41; ](../../t-sql/queries/search-condition-transact-sql.md).  
  
 \<table_hint_limited >  
 Especifica uma ou mais dicas de tabela que são aplicadas à tabela de destino para cada uma das ações de inserção, atualização ou exclusão executadas pela instrução MERGE. A palavra-chave WITH e parênteses são necessários.  
  
 NOLOCK e READUNCOMMITTED não são permitidos. Para obter mais informações sobre dicas de tabela, consulte [dicas de tabela &#40; Transact-SQL &#41; ](../../t-sql/queries/hints-transact-sql-table.md).  
  
 Especificar a dica TABLOCK em uma tabela que é o destino de uma instrução INSERT tem o mesmo efeito de especificar a dica TABLOCKX. Um bloqueio exclusivo é obtido na tabela. Quando FORCESEEK é especificada, ela é aplicada a uma instância implícita da tabela de destino unida à tabela de origem.  
  
> [!CAUTION]  
>  Especificar READPAST com WHEN NOT MATCHED [ BY TARGET ] THEN INSERT pode resultar em operações INSERT que violam restrições UNIQUE.  
  
 INDEX ( index_val [ ,...n ] )  
 Especifica o nome ou a identificação de um ou mais índices em uma tabela de destino para a execução de uma junção implícita com a tabela de origem. Para obter mais informações, consulte [Dicas de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 \<output_clause >  
 Retorna uma linha para cada linha na *target_table* que é atualizado, inserida ou excluída em nenhuma ordem específica. **$action** pode ser especificado na cláusula output. **$action** é uma coluna do tipo **nvarchar (10)** que retorna um dos três valores para cada linha: 'INSERT', 'UPDATE' ou 'DELETE', de acordo com a ação que foi executada na linha. Para obter mais informações sobre os argumentos dessa cláusula, consulte [cláusula OUTPUT &#40; Transact-SQL &#41; ](../../t-sql/queries/output-clause-transact-sql.md).  
  
 OPÇÃO ( \<query_hint > [,... n])  
 Especifica que dicas do otimizador são usadas para personalizar o modo como o Mecanismo de Banco de Dados processa a instrução. Para obter mais informações, veja [Dicas de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
 \<merge_matched >  
 Especifica a atualização ou excluir a ação que é aplicada a todas as linhas de *target_table* que não correspondem às linhas retornadas por \<table_source > ON \<merge_search_condition >, e que atendem a qualquer critério de pesquisa adicional.  
  
 UPDATE definida \<set_clause >  
 Especifica a lista de nomes de colunas ou de variáveis que devem ser atualizados na tabela de destino e os valores que devem ser usados na atualização.  
  
 Para obter mais informações sobre os argumentos dessa cláusula, consulte [UPDATE &#40; Transact-SQL &#41; ](../../t-sql/queries/update-transact-sql.md). Não é permitido definir o mesmo valor de uma coluna para uma variável.  
  
 DELETE  
 Especifica que as linhas que correspondem a linhas em *target_table* são excluídos.  
  
 \<merge_not_matched >  
 Especifica os valores a serem inseridos na tabela de destino.  
  
 (*column_list*)  
 É uma lista de uma ou mais colunas da tabela de destino na qual os dados devem ser inseridos. As colunas devem ser especificadas como um nome de parte única. Caso contrário, haverá falha na instrução MERGE. *column_list* devem ser colocados entre parênteses e delimitado por vírgulas.  
  
 VALORES ( *values_list*)  
 É uma lista de constantes, variáveis ou expressões separadas por vírgulas que retorna valores a serem inseridos na tabela de destino. As expressões não podem conter uma instrução EXECUTE.  
  
 DEFAULT VALUES  
 Força a linha inserida a conter os valores padrão definidos para cada coluna.  
  
 Para obter mais informações sobre essa cláusula, consulte [INSERT &#40; Transact-SQL &#41; ](../../t-sql/statements/insert-transact-sql.md).  
  
 \<critério de pesquisa >  
 Especifica as condições de pesquisa usadas para especificar \<merge_search_condition > ou \<clause_search_condition >. Para obter mais informações sobre os argumentos para essa cláusula, consulte [critério de pesquisa &#40; Transact-SQL &#41; ](../../t-sql/queries/search-condition-transact-sql.md).  
  
## <a name="remarks"></a>Comentários  
 Pelo menos uma das três cláusulas MATCHED devem ser especificadas, mas elas podem ser especificadas em qualquer ordem. Uma variável não pode ser atualizada mais de uma vez na mesma cláusula MATCHED.  
  
 Qualquer ação de inserção, atualização ou exclusão especificada na tabela de destino pela instrução MERGE é limitada pelas restrições definidas nela, incluindo qualquer restrição de integridade referencial em cascata. Se IGNORE_DUP_KEY for definida como ON em qualquer índice exclusivo na tabela de destino, MERGE ignorará esta configuração.  
  
 A instrução MERGE exige um ponto-e-vírgula (;) como terminador de instrução. O erro 10713 ocorre quando uma instrução MERGE é executada sem o terminador.  
  
 Quando usado após a mesclagem, [@@ROWCOUNT &#40; Transact-SQL &#41; ](../../t-sql/functions/rowcount-transact-sql.md) retorna o número total de linhas inseridas, atualizadas e excluídas para o cliente.  
  
 MERGE é uma palavra-chave totalmente reservada quando o nível de compatibilidade do banco de dados é definido como 100 ou superior. A instrução MERGE está disponível abaixo dos níveis de compatibilidade do banco de dados 90 e 100. No entanto, a palavra-chave não é totalmente reservada quando o nível de compatibilidade do banco de dados está definido como 90.  
  
 O **mesclar** instrução não deve ser usada quando usando replicação de atualização enfileirada. O **mesclagem** e o gatilho de atualização na fila não são compatíveis. Substitua o **mesclar** instrução com uma inserção ou uma instrução update.  
  
## <a name="trigger-implementation"></a>Implementação de gatilho  
 Para cada ação de inserção, atualização ou exclusão especificada na instrução MERGE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dispara qualquer gatilho AFTER correspondente definido na tabela de destino, mas não garante em qual ação os gatilhos serão disparados primeiro ou por último. Os gatilhos definidos para a mesma ação respeitam a ordem que você especifica. Para obter mais informações sobre como definir a ordem de acionamento do gatilho, consulte [especificar primeiro e últimos gatilhos](../../relational-databases/triggers/specify-first-and-last-triggers.md).  
  
 Se a tabela de destino tiver um gatilho INSTEAD OF habilitado definido para uma ação de inserção, atualização ou exclusão executada por uma instrução MERGE, ela deverá ter um gatilho INSTEAD OF habilitado para todas as ações especificadas na instrução MERGE.  
  
 Se houver qualquer gatilho INSTEAD OF UPDATE ou INSTEAD OF DELETE definido na *target_table*, as operações update ou delete não são executadas. Em vez disso, os gatilhos são disparados e **inserido** e **excluído** tabelas são preenchidas adequadamente.  
  
 Se houver, em vez de disparadores de inserção definidos na *target_table*, não é possível executar a operação de inserção. Em vez disso, os gatilhos são disparados e **inserido** tabela é populada de forma correspondente.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT na tabela de origem e as permissões INSERT, UPDATE ou DELETE na tabela de destino. Para obter mais informações, consulte a seção permissões a [selecione](../../t-sql/queries/select-transact-sql.md), [inserir](../../t-sql/statements/insert-transact-sql.md), [atualização](../../t-sql/queries/update-transact-sql.md), e [excluir](../../t-sql/statements/delete-transact-sql.md) tópicos.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-merge-to-perform-insert-and-update-operations-on-a-table-in-a-single-statement"></a>A. Usando MERGE para executar operações INSERT e UPDATE em uma tabela em uma única instrução  
 Um cenário comum é atualizar uma ou mais colunas em uma tabela, se uma linha correspondente existir, ou inserir os dados como uma nova linha, se uma linha correspondente não existir. Isto normalmente é feito transmitindo parâmetros para um procedimento armazenado que contém as instruções UPDATE e INSERT apropriadas. Com a instrução MERGE, você pode executar as duas tarefas em uma única instrução. O exemplo a seguir mostra um procedimento armazenado no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] que contém as instruções INSERT e UPDATE. Em seguida, o procedimento é modificado para executar as operações equivalentes usando uma única instrução MERGE.  
  
```  
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
  
### <a name="b-using-merge-to-perform-update-and-delete-operations-on-a-table-in-a-single-statement"></a>B. Usando MERGE para executar as operações UPDATE e DELETE em uma tabela em uma única instrução  
 O exemplo a seguir usa MERGE para atualizar diariamente a tabela `ProductInventory` no banco de dados de exemplo da [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] com base em pedidos processados na tabela `SalesOrderDetail`. A coluna `Quantity` da tabela `ProductInventory` foi atualizada subtraindo o número de pedidos colocados a cada dia para cada produto na tabela `SalesOrderDetail`. Se o número de pedidos de um produto reduzir o nível de estoque de um produto para 0 ou menos, a linha desse produto será excluída da tabela `ProductInventory`.  
  
```  
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
  
### <a name="c-using-merge-to-perform-update-and-insert-operations-on-a-target-table-by-using-a-derived-source-table"></a>C. Usando MERGE para executar as operações UPDATE e INSERT em uma tabela de destino usando uma tabela de origem derivada  
 O exemplo a seguir usa MERGE para modificar a tabela `SalesReason` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] atualizando ou inserindo linhas. Quando o valor de `NewName` na tabela de origem corresponde a um valor na coluna `Name` da tabela de destino (`SalesReason`), a coluna `ReasonType` é atualizada na tabela de destino. Quando o valor de `NewName` não corresponde, a linha de origem é inserida na tabela de destino. A tabela de origem é uma tabela derivada que usa o construtor de valor de tabela do [!INCLUDE[tsql](../../includes/tsql-md.md)] para especificar várias linhas para a tabela de origem. Para obter mais informações sobre como usar o construtor de valor de tabela em uma tabela derivada, consulte [construtor de valor de tabela &#40; Transact-SQL &#41; ](../../t-sql/queries/table-value-constructor-transact-sql.md). O exemplo também mostra como armazenar os resultados da cláusula OUTPUT em uma variável de tabela e resumir os resultados da instrução MERGE executando uma operação de seleção simples que retorna a contagem de linhas inseridas e atualizadas.  
  
```  
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
  
```  
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
  
## <a name="see-also"></a>Consulte também  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [Cláusula OUTPUT &#40; Transact-SQL &#41;](../../t-sql/queries/output-clause-transact-sql.md)   
 [MESCLAGEM de pacotes do Integration Services](../../integration-services/control-flow/merge-in-integration-services-packages.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [Construtor de valor de tabela &#40; Transact-SQL &#41;](../../t-sql/queries/table-value-constructor-transact-sql.md)  
  
  

