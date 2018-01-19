---
title: SELECT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/24/2017
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
- SELECT_TSQL
- SELECT
dev_langs: TSQL
helpviewer_keywords:
- retrieving rows
- SELECT statement [SQL Server]
- SELECT statement [SQL Server], about SELECT statement
- row retrieval [SQL Server], SELECT statement
- DML [SQL Server], SELECT statement
- data manipulation language [SQL Server], SELECT statement
- row retrieval [SQL Server]
- queries [SQL Server], results
ms.assetid: dc85caea-54d1-49af-b166-f3aa2f3a93d0
caps.latest.revision: "51"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 6dba1b14498cef9e06d9bde5741cb9e37cd31633
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="select-transact-sql"></a>SELECT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Recupera linhas do banco de dados e permite a seleção de uma ou várias linhas ou colunas de uma ou várias tabelas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A sintaxe completa da instrução SELECT é complexa, mas as cláusulas principais podem ser assim resumidas:  
  
[Com {[WITH XMLNAMESPACES,] [ \<common_table_expression >]}]
  
 SELECT *select_list* [ INTO *new_table* ]  
  
 [ FROM *table_source* ] [ WHERE *search_condition* ]  
  
 [ GROUP BY *group_by_expression* ]  
  
 [Tendo *search_condition* ]  
  
 [ORDER BY *order_expression* [ASC | DESC]]  
  
 A UNION, EXCEPT e INTERSECT operadores podem ser usados entre consultas para combinar ou comparar os resultados em um conjunto de resultados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
<SELECT statement> ::=    
    [ WITH { [ XMLNAMESPACES ,] [ <common_table_expression> [,...n] ] } ]  
    <query_expression>   
    [ ORDER BY { order_by_expression | column_position [ ASC | DESC ] }   
  [ ,...n ] ]   
    [ <FOR Clause>]   
    [ OPTION ( <query_hint> [ ,...n ] ) ]   
<query_expression> ::=   
    { <query_specification> | ( <query_expression> ) }   
    [  { UNION [ ALL ] | EXCEPT | INTERSECT }  
        <query_specification> | ( <query_expression> ) [...n ] ]   
<query_specification> ::=   
SELECT [ ALL | DISTINCT ]   
    [TOP ( expression ) [PERCENT] [ WITH TIES ] ]   
    < select_list >   
    [ INTO new_table ]   
    [ FROM { <table_source> } [ ,...n ] ]   
    [ WHERE <search_condition> ]   
    [ <GROUP BY> ]   
    [ HAVING < search_condition > ]   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
[ WITH <common_table_expression> [ ,...n ] ]  
SELECT <select_criteria>  
[;]  
  
<select_criteria> ::=  
    [ TOP ( top_expression ) ]   
    [ ALL | DISTINCT ]   
    { * | column_name | expression } [ ,...n ]   
    [ FROM { table_source } [ ,...n ] ]  
    [ WHERE <search_condition> ]   
    [ GROUP BY <group_by_clause> ]   
    [ HAVING <search_condition> ]   
    [ ORDER BY <order_by_expression> ]  
    [ OPTION ( <query_option> [ ,...n ] ) ]  
  
```  
  
## <a name="remarks"></a>Remarks  
 Devido à complexidade da instrução SELECT, os elementos e argumentos de sintaxe detalhados são mostrados por cláusula:  
  
|||  
|-|-|  
|[WITH XMLNAMESPACES](../../t-sql/xml/with-xmlnamespaces.md)<br /><br /> [WITH common_table_expression](../../t-sql/queries/with-common-table-expression-transact-sql.md)|[TENDO](../../t-sql/queries/select-having-transact-sql.md)|  
|[Cláusula SELECT](../../t-sql/queries/select-clause-transact-sql.md)|[UNIÃO](../../t-sql/language-elements/set-operators-union-transact-sql.md)|  
|[Cláusula INTO](../../t-sql/queries/select-into-clause-transact-sql.md)|[EXCEPT e INTERSECT](../../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)|  
|[FROM](../../t-sql/queries/from-transact-sql.md)|[ORDENAR POR](../../t-sql/queries/select-order-by-clause-transact-sql.md)|  
|[WHERE](../../t-sql/queries/where-transact-sql.md)|[Cláusula FOR](../../t-sql/queries/select-for-clause-transact-sql.md)|  
|[AGRUPAR POR](../../t-sql/queries/select-group-by-transact-sql.md)|[Cláusula OPTION](../../t-sql/queries/option-clause-transact-sql.md)|  
  
 A ordem das cláusulas na instrução SELECT é significativa. Qualquer uma das cláusulas opcionais pode ser omitida, mas quando elas são usadas devem aparecer na ordem apropriada.  
  
 As instruções SELECT serão permitidas em funções definidas pelo usuário apenas se as listas de seleção dessas instruções contiverem expressões que atribuam valores a variáveis que são locais a essas funções.  
  
 Um nome de quatro partes construído com a função OPENDATASOURCE como a parte do nome do servidor pode ser usado como uma origem de tabela sempre que um nome de tabela puder aparecer em uma instrução SELECT. Não é possível especificar um nome de quatro partes [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Algumas restrições de sintaxe se aplicam a instruções SELECT que envolvem tabelas remotas.  
  
## <a name="logical-processing-order-of-the-select-statement"></a>Ordem de processamento lógico da instrução SELECT  
 As etapas a seguir mostram a ordem de processamento lógico ou a ordem de associação de uma instrução SELECT. Essa ordem determina quando os objetos definidos em uma etapa são disponibilizados para as cláusulas em etapas subsequentes. Por exemplo, se o processador de consulta puder ser associado (acessar) a tabelas ou exibições definidas na cláusula FROM, esses objetos e suas colunas serão disponibilizados para todas as etapas subsequentes. De modo oposto, como a cláusula SELECT é a etapa 8, qualquer alias de coluna ou coluna derivada definida naquela cláusula não poderá ser referenciada por cláusulas precedentes. Porém, poderão ser referenciadas por cláusulas subsequentes, como a cláusula ORDER BY. A execução física real da instrução é determinada pelo processador de consulta e a ordem pode variar desta lista.  
  
1.  FROM  
2.  ON  
3.  JOIN  
4.  WHERE  
5.  GROUP BY  
6.  WITH CUBE ou WITH ROLLUP  
7.  HAVING  
8.  SELECT  
9. DISTINCT  
10. ORDER BY  
11. INÍCIO  

> [!WARNING]
> A sequência anterior geralmente é verdadeira. No entanto, há casos incomuns em que a sequência pode ser diferente.
>
> Por exemplo, suponha que você tem um índice clusterizado em uma exibição e o modo de exibição exclui algumas linhas de tabela e lista de colunas SELECT da exibição usa uma CONVERSÃO de um tipo de dados é alterado *varchar* para *inteiro*. Nessa situação, CONVERT pode ser executada antes da cláusula WHERE executa. Incomum de fato. Geralmente, há uma maneira de modificar sua exibição para evitar a sequência diferente, se for importante em seu caso. 

## <a name="permissions"></a>Permissões  
 A seleção de dados exige a permissão **SELECT** na tabela ou exibição, que pode ser herdada de um escopo superior, como a permissão **SELECT** no esquema ou a permissão **CONTROL** na tabela. Ou exige a associação no **db_datareader** ou **db_owner** funções de banco de dados fixas ou **sysadmin** função de servidor fixa. Criar uma nova tabela usando **SELECTINTO** também requer o **CREATETABLE** permissão e o **ALTERSCHEMA** permissão no esquema que possui a nova tabela.  
  
## <a name="examples"></a>Exemplos:   
Os exemplos a seguir usam o [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] banco de dados.
  
### <a name="a-using-select-to-retrieve-rows-and-columns"></a>A. Usando SELECT para recuperar linhas e colunas  
 Esta seção mostra três exemplos de código. Este primeiro exemplo de código retorna todas as linhas (nenhuma cláusula WHERE é especificada) e todas as colunas (usando o `*`) da `DimEmployee` tabela.  
  
```sql  
SELECT *  
FROM DimEmployee  
ORDER BY LastName;  
```  
  
 Este próximo exemplo usando o alias de tabela para obter o mesmo resultado.  
  
```sql  
SELECT e.*  
FROM DimEmployee AS e  
ORDER BY LastName;  
```  
  
 Este exemplo retorna todas as linhas (nenhuma cláusula WHERE é especificada) e um subconjunto das colunas (`FirstName`, `LastName`, `StartDate`) da `DimEmployee` tabela o `AdventureWorksPDW2012` banco de dados. Título da terceiro coluna é renomeado para `FirstDay`.  
  
```sql  
SELECT FirstName, LastName, StartDate AS FirstDay  
FROM DimEmployee   
ORDER BY LastName;  
```  
  
 Este exemplo retorna somente as linhas de `DimEmployee` que têm um `EndDate` que não seja NULL e uma `MaritalStatus` de estou ' (casado).  
  
```sql  
SELECT FirstName, LastName, StartDate AS FirstDay  
FROM DimEmployee   
WHERE EndDate IS NOT NULL   
AND MaritalStatus = 'M'  
ORDER BY LastName;  
```  
  
### <a name="b-using-select-with-column-headings-and-calculations"></a>B. Usando SELECT com títulos de coluna e cálculos  
 O exemplo a seguir retorna todas as linhas do `DimEmployee` da tabela e calcula o pagamento bruto para cada funcionário com base em seus `BaseRate` e 40 horas por semana.  
  
```sql  
SELECT FirstName, LastName, BaseRate, BaseRate * 40 AS GrossPay  
FROM DimEmployee  
ORDER BY LastName;  
```  
  
### <a name="c-using-distinct-with-select"></a>C. Usando DISTINCT com SELECT  
 O exemplo a seguir usa `DISTINCT` para gerar uma lista de todos os títulos exclusivos a `DimEmployee` tabela.  
  
```sql  
SELECT DISTINCT Title  
FROM DimEmployee  
ORDER BY Title;  
```  
  
### <a name="d-using-group-by"></a>D. Usando GROUP BY  
 O exemplo a seguir localiza a quantidade total de todas as vendas em cada dia.  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey  
ORDER BY OrderDateKey;  
```  
  
 Devido a `GROUP BY` cláusula, somente uma linha que contém a soma de todas as vendas é retornada para cada dia.  
  
### <a name="e-using-group-by-with-multiple-groups"></a>E. Usando GROUP BY com vários grupos  
 O exemplo a seguir localiza o preço médio e a soma de vendas pela Internet para cada dia, agrupados por data do pedido e a chave de promoção.  
  
```sql  

SELECT OrderDateKey, PromotionKey, AVG(SalesAmount) AS AvgSales, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey, PromotionKey  
ORDER BY OrderDateKey;   
```  
  
### <a name="f-using-group-by-and-where"></a>F. Usando GROUP BY e WHERE  
 O exemplo a seguir coloca os resultados em grupos depois de recuperar somente as linhas com datas de pedido posterior a 1º de agosto de 2002.  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
WHERE OrderDateKey > '20020801'  
GROUP BY OrderDateKey  
ORDER BY OrderDateKey;  
```  
  
### <a name="g-using-group-by-with-an-expression"></a>G. Usando GROUP BY com uma expressão  
 O exemplo a seguir agrupa por uma expressão. É possível agrupar por uma expressão se a mesma não contiver funções de agregação.  
  
```sql  
SELECT SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY (OrderDateKey * 10);  
```  
  
### <a name="h-using-group-by-with-order-by"></a>H. Usando GROUP BY com ORDER BY  
 O exemplo a seguir localiza a soma das vendas por dia e pedidos por dia.  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey  
ORDER BY OrderDateKey;  
```  
  
### <a name="i-using-the-having-clause"></a>I. Usando a cláusula HAVING  
 Essa consulta usa o `HAVING` cláusula para restringir os resultados.  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey  
HAVING OrderDateKey > 20010000  
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exemplos SELECT &#40; Transact-SQL &#41;](../../t-sql/queries/select-examples-transact-sql.md)  
 [Hints &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql.md)
  

