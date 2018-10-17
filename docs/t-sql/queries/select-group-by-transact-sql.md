---
title: GROUP BY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GROUP
- CUBE
- ROLLUP
- GROUPING_SETS_TSQL
- GROUP BY
- GROUPING SETS
- GROUP_BY_TSQL
- GROUP_TSQL
- CUBE_TSQL
- ROLLUP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GROUP BY clause, about GROUP BY clause
- dividing tables into groups
- GROUPING SETS
- GROUP BY clause
- table groups [SQL Server]
- groups [SQL Server], tables divided into groups
- summary values [SQL Server]
ms.assetid: 40075914-6385-4692-b4a5-62fe44ae6cb6
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cd0f0157f1f3f0c684dcb8f07af725b97929c10f
ms.sourcegitcommit: 110e5e09ab3f301c530c3f6363013239febf0ce5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48906016"
---
# <a name="select---group-by--transact-sql"></a>SELECT – GROUP BY – Transact-SQL
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Uma cláusula da instrução SELECT que divide o resultado da consulta em grupos de linhas, normalmente, com a finalidade de executar uma ou mais agregações em cada grupo. A instrução SELECT retorna uma linha por grupo.  
  
## <a name="syntax"></a>Sintaxe  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
```  
-- Syntax for SQL Server and Azure SQL Database   
-- ISO-Compliant Syntax  
  
GROUP BY {
      column-expression  
    | ROLLUP ( <group_by_expression> [ ,...n ] )  
    | CUBE ( <group_by_expression> [ ,...n ] )  
    | GROUPING SETS ( <grouping_set> [ ,...n ]  )  
    | () --calculates the grand total 
} [ ,...n ] 
 
<group_by_expression> ::=  
      column-expression  
    | ( column-expression [ ,...n ] )    
   
<grouping_set> ::=  
      () --calculates the grand total  
    | <grouping_set_item>  
    | ( <grouping_set_item> [ ,...n ] )  
  
<grouping_set_item> ::=  
      <group_by_expression>  
    | ROLLUP ( <group_by_expression> [ ,...n ] )  
    | CUBE ( <group_by_expression> [ ,...n ] )  
  

-- For backward compatibility only.
-- Non-ISO-Compliant Syntax for SQL Server and Azure SQL Database 
  
GROUP BY 
      [ ALL ] column-expression [ ,...n ] 
    | column-expression [ ,...n ] [ WITH { CUBE | ROLLUP } ]   

```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
GROUP BY {
      column-name [ WITH (DISTRIBUTED_AGG) ]  
    | column-expression
} [ ,...n ]

```  
  
## <a name="arguments"></a>Argumentos 
 
### <a name="column-expression"></a>*column-expression*  
Especifica uma coluna ou um cálculo de não agregação em uma coluna. Essa coluna pode pertencer a uma tabela, a uma tabela derivada ou a uma exibição. A coluna precisa aparecer na cláusula FROM da instrução SELECT, mas não precisa aparecer na lista de SELECT. 

Para saber quais são as expressões válidas, confira [Expressão](~/t-sql/language-elements/expressions-transact-sql.md).    

A coluna precisa aparecer na cláusula FROM da instrução SELECT, mas não precisa aparecer na lista de SELECT. No entanto, cada coluna de tabela ou de exibição em qualquer expressão de não agregação na lista de \<select> precisa estar incluída na lista de GROUP BY:  
  
As seguintes instruções são permitidas:  
  
```sql  
SELECT ColumnA, ColumnB FROM T GROUP BY ColumnA, ColumnB;  
SELECT ColumnA + ColumnB FROM T GROUP BY ColumnA, ColumnB;  
SELECT ColumnA + ColumnB FROM T GROUP BY ColumnA + ColumnB;  
SELECT ColumnA + ColumnB + constant FROM T GROUP BY ColumnA, ColumnB;  
```  
  
As seguintes instruções não são permitidas:  
  
```sql  
SELECT ColumnA, ColumnB FROM T GROUP BY ColumnA + ColumnB;  
SELECT ColumnA + constant + ColumnB FROM T GROUP BY ColumnA + ColumnB;  
```  

A expressão de coluna não pode conter:

- Um alias de coluna definido na lista de SELECT. Ela pode usar um alias de coluna para uma tabela derivada definida na cláusula FROM.
- Uma coluna do tipo **text**, **ntext** ou **image**. No entanto, você pode usar uma coluna de texto, ntext ou imagem como um argumento para uma função que retorna um valor de um tipo de dados válido. Por exemplo, a expressão pode usar SUBSTRING() e CAST(). Isso também se aplica às expressões na cláusula HAVING.
- Métodos do tipo de dados XML. Ela pode incluir uma função definida pelo usuário que usa métodos do tipo de dados XML. Ela pode incluir uma coluna computada que usa métodos do tipo de dados XML. 
- Uma subconsulta. O erro 144 é retornado. 
- Uma coluna de uma exibição indexada. 
 
### <a name="group-by-column-expression--n-"></a>GROUP BY *column-expression* [ ,...n ] 

Agrupa os resultados da instrução SELECT de acordo com os valores em uma lista de uma ou mais expressões de coluna. 

Por exemplo, essa consulta cria a tabela Vendas com as colunas País, Região e Vendas. Ela insere quatro linhas e duas da linhas têm valores correspondentes para País e Região.  

```sql
CREATE TABLE Sales ( Country varchar(50), Region varchar(50), Sales int );

INSERT INTO sales VALUES (N'Canada', N'Alberta', 100);
INSERT INTO sales VALUES (N'Canada', N'British Columbia', 200);
INSERT INTO sales VALUES (N'Canada', N'British Columbia', 300);
INSERT INTO sales VALUES (N'United States', N'Montana', 100);
```
A tabela Vendas contém estas linhas:

| País | Região | Sales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| Canada | Colúmbia Britânica | 200 |
| Canada | Colúmbia Britânica | 300 |
| Estados Unidos | Montana | 100 |

Essa próxima consulta agrupa País e Região e retorna a soma de agregação para cada combinação de valores.  
 
```sql 
SELECT Country, Region, SUM(sales) AS TotalSales
FROM Sales
GROUP BY Country, Region;
```
O resultado da consulta tem 3 linhas, pois há 3 combinações de valores para País e Região. TotalSales para Canadá e Colúmbia Britânica é a soma de duas linhas. 

| País | Região | TotalSales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| Canada | Colúmbia Britânica | 500 |
| Estados Unidos | Montana | 100 |

### <a name="group-by-rollup"></a>GROUP BY ROLLUP

Cria um grupo para cada combinação de expressões de coluna. Além disso, ele "acumula" os resultados em subtotais e totais gerais. Para isso, ele vai da direita para a esquerda, diminuindo o número de expressões de coluna sobre as quais ele cria grupos e agregações. 

A ordem da coluna afeta a saída de ROLLUP e pode afetar o número de linhas no conjunto de resultados.  

Por exemplo, `GROUP BY ROLLUP (col1, col2, col3, col4)` cria grupos para cada combinação de expressões de coluna nas listas a seguir.  

- col1, col2, col3, col4 
- col1, col2, col3, NULL
- col1, col2, NULL, NULL
- col1, NULL, NULL, NULL
- NULL, NULL, NULL, NULL – esse é o total geral

Usando a tabela do exemplo anterior, esse código executa uma operação de GROUP BY ROLLUP em vez de um GROUP BY simples.

```sql
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY ROLLUP (Country, Region);
```

O resultado da consulta tem as mesmas agregações que o GROUP BY simples sem o ROLLUP. Além disso, ele cria subtotais para cada valor de País. Por fim, ele fornece um total geral para todas as linhas. O resultado será semelhante a este:

| País | Região | TotalSales |
| :------ | :----- | ---------: |
| Canada | Alberta | 100 |
| Canada | Colúmbia Britânica | 500 |
| Canada | NULL | 600 |
| Estados Unidos | Montana | 100 |
| Estados Unidos | NULL | 100 |
| NULL | NULL | 700 |

### <a name="group-by-cube--"></a>GROUP BY CUBE ( )  

GROUP BY CUBE cria grupos para todas as combinações de colunas possíveis. GROUP BY CUBE (a, b) os resultados têm grupos de valores exclusivos de (a, b), (NULL, b), (a, NULL) e (NULL, NULL).

Usando a tabela dos exemplos anteriores, esse código executa uma operação de GROUP BY CUBE em País e em Região. 

```sql
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY CUBE (Country, Region);
```

O resultado da consulta tem grupos de valores exclusivos (País, Região), (NULL, Região), (País, NULL) e (NULL, NULL). Os resultados serão semelhantes a estes:

| País | Região | TotalSales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| NULL | Alberta | 100 |
| Canada | Colúmbia Britânica | 500 |
| NULL | Colúmbia Britânica | 500 |
| Estados Unidos | Montana | 100 |
| NULL | Montana | 100 |
| NULL | NULL | 700
| Canada | NULL | 600 |
| Estados Unidos | NULL | 100 |
   
 ### <a name="group-by-grouping-sets--"></a>GROUP BY GROUPING SETS ( )  
 
A opção de GROUPING SETS oferece a capacidade de combinar várias cláusulas GROUP BY em uma única cláusula GROUP BY. Os resultados são o equivalente de UNION ALL dos grupos especificados. 

Por exemplo, `GROUP BY ROLLUP (Country, Region)` e `GROUP BY GROUPING SETS ( ROLLUP (Country, Region) )` retornam os mesmos resultados. 

Quando conjuntos de GROUPING SETS têm dois ou mais elementos, os resultados são uma união dos elementos. Este exemplo retorna a união dos resultados de ROLLUP e CUBE para País e Região.

```sql
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY GROUPING SETS ( ROLLUP (Country, Region), CUBE (Country, Region) );
```

Os resultados são iguais, pois essa consulta retorna uma união de duas instruções GROUP BY.

```sql
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY ROLLUP (Country, Region)
UNION ALL
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY CUBE (Country, Region);
```

O SQL não consolida grupos duplicados gerados por uma lista de GROUPING SETS. Por exemplo, em `GROUP BY ( (), CUBE (Country, Region) )`, ambos os elementos retornarão uma linha para o total geral e ambas as linhas serão listadas nos resultados. 

 ### <a name="group-by-"></a>GROUP BY ()  
Especifica o grupo vazio que gera o total geral. Isso é útil como um dos elementos de um GROUPING SET. Por exemplo, esta instrução fornece o total de vendas para cada país e, em seguida, o total geral para todos os países.

```sql
SELECT Country, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY GROUPING SETS ( Country, () );
```

### <a name="group-by--all--column-expression--n-"></a>GROUP BY [ ALL ] column-expression [ ,...n ] 

Aplica-se a: SQL Server e Banco de Dados SQL do Azure

Observação: esta sintaxe é fornecida apenas para fins de compatibilidade com versões anteriores. Ela será removida em uma versão futura. Evite usar essa sintaxe em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que a usam no momento.

Especifica a inclusão de todos os grupos nos resultados, independentemente se eles atendem aos critérios de pesquisa na cláusula WHERE. Os grupos que não atendem aos critérios de pesquisa têm NULL para a agregação. 

GROUP BY ALL:
- Não é compatível com consultas que acessam tabelas remotas quando também há uma cláusula WHERE na consulta.
- Falhará em colunas que têm o atributo FILESTREAM.
  
### <a name="with-distributedagg"></a>WITH (DISTRIBUTED_AGG)
Aplica-se a: SQL Data Warehouse do Azure e Parallel Data Warehouse

A dica de consulta DISTRIBUTED_AGG força o sistema de MPP (processamento paralelo massivo) a redistribuir uma tabela em uma coluna específica antes de executar uma agregação. Somente uma coluna na cláusula GROUP BY pode ter uma dica de consulta DISTRIBUTED_AGG. Depois que a consulta for concluída, a tabela redistribuída será descartada. A tabela original não é alterada.  

Observação: a dica de consulta DISTRIBUTED_AGG é fornecida para fins de compatibilidade com versões anteriores do Parallel Data Warehouse e não melhora o desempenho na maioria das consultas. Por padrão, o MPP já redistribui os dados conforme o necessário para melhorar o desempenho das agregações. 
  
## <a name="general-remarks"></a>Comentários gerais

### <a name="how-group-by-interacts-with-the-select-statement"></a>Como GROUP BY interage com a instrução SELECT
Lista de SELECT:
- Agregações de vetor. Se funções de agregação são incluídas na lista de SELECT, GROUP BY calcula um valor resumido para cada grupo. São conhecidas como agregações de vetor. 
- Agregações de distinção. As agregações AVG (DISTINCT *column_name*), COUNT (DISTINCT *column_name*) e SUM (DISTINCT *column_name*) são compatíveis com ROLLUP, CUBE e GROUPING SETS.
  
Cláusula WHERE:
- O SQL remove as linhas que não atendem às condições na cláusula WHERE antes que qualquer operação de agrupamento seja executada.  
  
Cláusula HAVING:
- O SQL usa a cláusula having para filtrar grupos no conjunto de resultados. 
  
Cláusula ORDER BY:
- Use a cláusula ORDER BY para ordenar o conjunto de resultados. A cláusula GROUP BY não ordena o conjunto de resultados. 
  
Valores NULL:
- Se uma coluna de agrupamento contiver valores NULL, todos os valores NULL serão considerados iguais e serão coletados em um único grupo.   
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições

Aplica-se a: SQL Server (começando com o 2008) e SQL Data Warehouse do Azure

### <a name="maximum-capacity"></a>Capacidade máxima

Para uma cláusula GROUP BY que usa ROLLUP, CUBE ou GROUPING SETS, o número máximo de expressões é 32. O número máximo de grupos é 4096 (2<sup>12</sup>). Os exemplos a seguir falham porque a cláusula GROUP BY tem mais de 4096 grupos.  
 
-   O exemplo a seguir gera 4097 (2<sup>12</sup> + 1) conjuntos de agrupamentos e falhará.  
  
    ```sql
    GROUP BY GROUPING SETS( CUBE(a1, ..., a12), b )  
    ```  
  
-   O exemplo a seguir gera 4097 (2<sup>12</sup> + 1) grupos e falhará. `CUBE ()` e o conjunto de agrupamentos `()` produzem uma linha de total geral e os conjuntos de agrupamentos duplicados não são eliminados.  
  
    ```sql
    GROUP BY GROUPING SETS( CUBE(a1, ..., a12), ())  
    ```  

-   Este exemplo usa a sintaxe compatível com versões anteriores. Ele gera 8192 (2<sup>13</sup>) conjuntos de agrupamentos e falhará.  
  
    ```sql
    GROUP BY CUBE (a1, ..., a13)   
    GROUP BY a1, ..., a13 WITH CUBE   
    ```    
    Para cláusulas GROUP BY compatíveis com versões anteriores que não contêm CUBE nem ROLLUP, o número de itens de group by é limitado pelos tamanhos da coluna GROUP BY, pelas colunas agregadas e pelos valores de agregação envolvidos na consulta. Esse limite tem origem no limite de 8.060 bytes na tabela de trabalho intermediária que é necessária para manter resultados de consulta intermediários. Um máximo de 12 expressões de agrupamento é permitido quando CUBE ou ROLLUP é especificado.

### <a name="support-for-iso-and-ansi-sql-2006-group-by-features"></a>Suporte para os recursos GROUP BY ISO e ANSI SQL-2006

A cláusula GROUP BY é compatível com todos os recursos de GROUP BY incluídos no padrão SQL-2006 com as seguintes exceções de sintaxe:  
  
-   Conjuntos de agrupamentos não são permitidos na cláusula GROUP BY, a menos que sejam parte de uma lista de GROUPING SETS explícita. Por exemplo, `GROUP BY Column1, (Column2, ...ColumnN`) é permitido no padrão, mas não no Transact-SQL.  O Transact-SQL é compatível com `GROUP BY C1, GROUPING SETS ((Column2, ...ColumnN))` e `GROUP BY Column1, Column2, ... ColumnN`, que são semanticamente equivalentes. Esses são semanticamente equivalentes ao exemplo `GROUP BY` anterior. Isso é para evitar a possibilidade de que `GROUP BY Column1, (Column2, ...ColumnN`) seja ser interpretado incorretamente como `GROUP BY C1, GROUPING SETS ((Column2, ...ColumnN))`, que não são semanticamente equivalentes.  
  
-   Conjuntos de agrupamentos não são permitidos em conjuntos de agrupamentos. Por exemplo, `GROUP BY GROUPING SETS (A1, A2,…An, GROUPING SETS (C1, C2, ...Cn))` é permitido no padrão SQL-2006, mas não no Transact-SQL. O Transact-SQL permite `GROUP BY GROUPING SETS( A1, A2,...An, C1, C2, ...Cn )` ou `GROUP BY GROUPING SETS( (A1), (A2), ... (An), (C1), (C2), ... (Cn) )`, que são semanticamente equivalentes ao primeiro exemplo de GROUP BY e têm uma sintaxe mais clara.  
  
-   GROUP BY [ALL/DISTINCT] só é permitido em uma cláusula GROUP BY simples que contém expressões de coluna. Ele não é permitido com as construções GROUPING SETS, ROLLUP, CUBE, WITH CUBE ou WITH ROLLUP. ALL é o padrão e está implícito. Ele também só é permitido na sintaxe compatível com versões anteriores.
  
### <a name="comparison-of-supported-group-by-features"></a>Comparação de recursos GROUP BY com suporte  
 A tabela a seguir descreve os recursos de GROUP BY compatíveis, com base nas versões do SQL e no nível de compatibilidade do banco de dados.  
  
|Recurso|SQL Server Integration Services|Nível de compatibilidade 100 ou superior do SQL Server|Nível de compatibilidade 90 do SQL Server 2008 ou posterior.|  
|-------------|-------------------------------------|--------------------------------------------------|-----------------------------------------------------------|  
|Agregações de DISTINCT|Não há suporte para WITH CUBE ou WITH ROLLUP.|Há suporte para WITH CUBE, WITH ROLLUP, GROUPING SETS, CUBE ou ROLLUP.|Igual ao nível de compatibilidade 100.|  
|Função definida pelo usuário com nome CUBE ou ROLLUP na cláusula GROUP BY|A função definida pelo usuário **dbo.cube(**_arg1_**,**_...argN_**)** ou **dbo.rollup(**_arg1_**,**..._argN_**)** na cláusula GROUP BY é permitida.<br /><br /> Por exemplo: `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`|A função definida pelo usuário **dbo.cube (**_arg1_**,**...argN **)** ou **dbo.rollup(** arg1 **,**_...argN_**)** na cláusula GROUP BY não é permitida.<br /><br /> Por exemplo: `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`<br /><br /> A seguinte mensagem de erro é retornada: "sintaxe incorreta próxima à palavra-chave 'cube'&#124;'rollup'".<br /><br /> Para evitar esse problema, substitua `dbo.cube` por `[dbo].[cube]` ou `dbo.rollup` por `[dbo].[rollup]`.<br /><br /> O exemplo a seguir é permitido: `SELECT SUM (x) FROM T  GROUP BY [dbo].[cube](y);`|A função definida pelo usuário **dbo.cube (**_arg1_**,**_...argN_) ou **dbo.rollup(**_arg1_**,**_...argN_**)** na cláusula GROUP BY é permitida<br /><br /> Por exemplo: `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`|  
|GROUPING SETS|Sem suporte|Tem suporte|Tem suporte|  
|CUBE|Sem suporte|Tem suporte|Sem suporte|  
|ROLLUP|Sem suporte|Tem suporte|Sem suporte|  
|Total geral, como GROUP BY ()|Sem suporte|Tem suporte|Tem suporte|  
|Função GROUPING_ID|Sem suporte|Tem suporte|Tem suporte|  
|função GROUPING|Tem suporte|Tem suporte|Tem suporte|  
|WITH CUBE|Tem suporte|Tem suporte|Tem suporte|  
|WITH ROLLUP|Tem suporte|Tem suporte|Tem suporte|  
|Remoção de agrupamento "duplicado" WITH CUBE ou WITH ROLLUP|Tem suporte|Tem suporte|Tem suporte| 
 
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-use-a-simple-group-by-clause"></a>A. Usar uma cláusula GROUP BY simples  
 O exemplo a seguir recupera o total para cada tabela `SalesOrderID` da tabela `SalesOrderDetail`. Este exemplo usa o AdventureWorks.  
  
```sql  
SELECT SalesOrderID, SUM(LineTotal) AS SubTotal  
FROM Sales.SalesOrderDetail AS sod  
GROUP BY SalesOrderID  
ORDER BY SalesOrderID;  
```  
  
### <a name="b-use-a-group-by-clause-with-multiple-tables"></a>B. Usar uma cláusula GROUP BY com várias tabelas  
 O exemplo a seguir recupera o número de funcionários de cada `City` da tabela `Address` unida à tabela `EmployeeAddress`. Este exemplo usa o AdventureWorks. 
  
```sql  
SELECT a.City, COUNT(bea.AddressID) EmployeeCount  
FROM Person.BusinessEntityAddress AS bea   
    INNER JOIN Person.Address AS a  
        ON bea.AddressID = a.AddressID  
GROUP BY a.City  
ORDER BY a.City;  
```  
  
### <a name="c-use-a-group-by-clause-with-an-expression"></a>C. Usar uma cláusula GROUP BY com uma expressão  
 O exemplo a seguir recupera as vendas totais durante cada ano usando a função `DATEPART`. A mesma expressão deve estar presente na lista `SELECT` e na cláusula `GROUP BY`.  
  
```sql  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,SUM(TotalDue) AS N'Total Order Amount'  
FROM Sales.SalesOrderHeader  
GROUP BY DATEPART(yyyy,OrderDate)  
ORDER BY DATEPART(yyyy,OrderDate);  
```  
  
### <a name="d-use-a-group-by-clause-with-a-having-clause"></a>D. Usar uma cláusula GROUP BY com uma cláusula HAVING  
 O exemplo a seguir usa a cláusula `HAVING` para especificar quais dos grupos gerados na cláusula `GROUP BY` devem ser incluídos no conjunto de resultados.  
  
```sql  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,SUM(TotalDue) AS N'Total Order Amount'  
FROM Sales.SalesOrderHeader  
GROUP BY DATEPART(yyyy,OrderDate)  
HAVING DATEPART(yyyy,OrderDate) >= N'2003'  
ORDER BY DATEPART(yyyy,OrderDate);  
```  
  
## <a name="examples-sql-data-warehouse-and-parallel-data-warehouse"></a>Exemplos: SQL Data Warehouse e Parallel Data Warehouse  
  
### <a name="e-basic-use-of-the-group-by-clause"></a>E. Uso básico da cláusula GROUP BY  
 O exemplo a seguir localiza a quantidade total de todas as vendas em cada dia. Uma linha que contém a soma de todas as vendas é retornada para cada dia.  
  
```sql  
-- Uses AdventureWorksDW  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales FROM FactInternetSales  
GROUP BY OrderDateKey ORDER BY OrderDateKey;  
```  
  
### <a name="f-basic-use-of-the-distributedagg-hint"></a>F. Uso básico da dica de DISTRIBUTED_AGG  
 Este exemplo usa a dica de consulta DISTRIBUTED_AGG para forçar o dispositivo a embaralhar a tabela na coluna `CustomerKey` antes de executar a agregação.  
  
```sql  
-- Uses AdventureWorksDW  
  
SELECT CustomerKey, SUM(SalesAmount) AS sas  
FROM FactInternetSales  
GROUP BY CustomerKey WITH (DISTRIBUTED_AGG)  
ORDER BY CustomerKey DESC;  
```  
  
### <a name="g-syntax-variations-for-group-by"></a>G. Variações de sintaxe para GROUP BY  
 Quando a lista de seleção não tem nenhuma agregação, cada coluna na lista de seleção precisa ser incluída na lista GROUP BY. As colunas computadas na lista de seleção podem ser listadas, mas não são obrigatórias na lista GROUP BY. Estes são exemplos de instruções SELECT sintaticamente válidas:  
  
```sql  
-- Uses AdventureWorks  
  
SELECT LastName, FirstName FROM DimCustomer GROUP BY LastName, FirstName;  
SELECT NumberCarsOwned FROM DimCustomer GROUP BY YearlyIncome, NumberCarsOwned;  
SELECT (SalesAmount + TaxAmt + Freight) AS TotalCost FROM FactInternetSales GROUP BY SalesAmount, TaxAmt, Freight;  
SELECT SalesAmount, SalesAmount*1.10 SalesTax FROM FactInternetSales GROUP BY SalesAmount;  
SELECT SalesAmount FROM FactInternetSales GROUP BY SalesAmount, SalesAmount*1.10;  
```  
  
### <a name="h-using-a-group-by-with-multiple-group-by-expressions"></a>H. Usando um GROUP BY com várias expressões GROUP BY  
 O exemplo a seguir agrupa os resultados usando vários critérios de `GROUP BY`. Se dentro de cada grupo `OrderDateKey` houver subgrupos que possam ser diferenciados pela `DueDateKey`, um novo agrupamento será definido para o conjunto de resultados.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, DueDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSales
GROUP BY OrderDateKey, DueDateKey   
ORDER BY OrderDateKey;  
```  
  
### <a name="i-using-a-group-by-clause-with-a-having-clause"></a>I. Usando uma cláusula GROUP BY com uma cláusula HAVING  
 O exemplo a seguir usa a cláusula `HAVING` para especificar os grupos gerados na cláusula `GROUP BY` que devem ser incluídos no conjunto de resultados. Somente os grupos com datas de pedido de 2004 ou posteriores serão incluídos nos resultados.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSales  
GROUP BY OrderDateKey   
HAVING OrderDateKey > 20040000   
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [GROUPING_ID &#40;Transact-SQL&#41;](~/t-sql/functions/grouping-id-transact-sql.md)   
 [GROUPING &#40;Transact-SQL&#41;](~/t-sql/functions/grouping-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](~/t-sql/queries/select-transact-sql.md)   
 [Cláusula SELECT &#40;Transact-SQL&#41;](~/t-sql/queries/select-clause-transact-sql.md)  
  
  




