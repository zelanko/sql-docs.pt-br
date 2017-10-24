---
title: Agrupar por (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 80
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 01e2c02cade5b84f3560fe5cb415cece4f815abf
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="select---group-by--transact-sql"></a>Selecione - BY - Transact-SQL GROUP
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Uma cláusula de instrução SELECT que divide o resultado da consulta em grupos de linhas, normalmente, para fins de executar um ou mais agregações em cada grupo. A instrução SELECT retorna uma linha por grupo.  
  
## <a name="syntax"></a>Sintaxe  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico") [convenções de sintaxe do Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
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
 
### <a name="column-expression"></a>*expressão de coluna*  
Especifica uma coluna ou um cálculo de não agregação em uma coluna. Esta coluna pode pertencer a uma tabela, uma tabela derivada ou uma exibição. A coluna deve aparecer na cláusula FROM da instrução SELECT, mas não é necessária para aparecer na lista de seleção. 

Para expressões válidas, consulte [expressão](~/t-sql/language-elements/expressions-transact-sql.md).    

A coluna deve aparecer na cláusula FROM da instrução SELECT, mas não é necessária para aparecer na lista de seleção. No entanto, cada tabela ou exibir a coluna em qualquer expressão não agregada no \<selecione > lista deve ser incluída na lista GROUP BY:  
  
As seguintes instruções são permitidas:  
  
    ```  
    SELECT ColumnA, ColumnB FROM T GROUP BY ColumnA, ColumnB;  
    SELECT ColumnA + ColumnB FROM T GROUP BY ColumnA, ColumnB;  
    SELECT ColumnA + ColumnB FROM T GROUP BY ColumnA + ColumnB;  
    SELECT ColumnA + ColumnB + constant FROM T GROUP BY ColumnA, ColumnB;  
    ```  
  
As seguintes instruções não são permitidas:  
  
    ```  
    SELECT ColumnA, ColumnB FROM T GROUP BY ColumnA + ColumnB;  
    SELECT ColumnA + constant + ColumnB FROM T GROUP BY ColumnA + ColumnB;  
    ```  
A expressão de coluna não pode conter:

- Um alias de coluna que está definido na lista de seleção. Ele pode usar um alias de coluna para uma tabela derivada que é definida na cláusula FROM.
- Uma coluna do tipo **texto**, **ntext**, ou **imagem**. No entanto, você pode usar uma coluna de text, ntext ou imagem como um argumento para uma função que retorna um valor de um tipo de dados válido. Por exemplo, a expressão pode usar substring () e cast (). Isso também se aplica a expressões na cláusula HAVING.
- métodos de tipo de dados XML. Ele pode incluir uma função definida pelo usuário que usa os métodos de tipo de dados xml. Ele pode incluir uma coluna computada que usa os métodos de tipo de dados xml. 
- Uma subconsulta. Erro 144 é retornado. 
- Uma coluna de uma exibição indexada. 
 
### <a name="group-by-column-expression--n-"></a>GROUP BY *expressão de coluna* [,... n] 

Agrupa os resultados da instrução SELECT acordo com os valores em uma lista de uma ou mais expressões de coluna. 

Por exemplo, esta consulta cria uma tabela de vendas com colunas de país, região e vendas. Ele insere quatro linhas e duas linhas têm valores correspondentes para país e região.  

```
CREATE TABLE Sales ( Country varchar(50), Region varchar(50), Sales int );

INSERT INTO sales VALUES (N'Canada', N'Alberta', 100);
INSERT INTO sales VALUES (N'Canada', N'British Columbia', 200);
INSERT INTO sales VALUES (N'Canada', N'British Columbia', 300);
INSERT INTO sales VALUES (N'United States', N'Montana', 100);
```
A tabela de vendas contém estas linhas:

| País | Região | Sales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| Canada | Colúmbia Britânica | 200 |
| Canada | Colúmbia Britânica | 300 |
| United States | Montana | 100 |

Essa consulta seguinte agrupa país e região e retorna a soma de agregação para cada combinação de valores.  
 
``` 
SELECT Country, Region, SUM(sales) AS TotalSales
FROM Sales
GROUP BY Country, Region;
```
O resultado da consulta tem 3 linhas, pois há 3 combinações de valores de país e região. TotalSales para o Canadá e a Colúmbia Britânica é a soma de duas linhas. 

| País | Região | TotalSales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| Canada | Colúmbia Britânica | 500 |
| United States | Montana | 100 |

### <a name="group-by-rollup"></a>GROUP BY ROLLUP

Cria um grupo para cada combinação de expressões de coluna. Além disso, ele "acumula" os resultados em subtotais e totais gerais. Para fazer isso, ele move da direita para esquerda, diminuindo o número de expressões de coluna durante o qual ele cria o aggregation(s) e grupos. 

A ordem da coluna afeta a saída do pacote cumulativo de atualizações e pode afetar o número de linhas no conjunto de resultados.  

Por exemplo, `GROUP BY ROLLUP (col1, col2, col3, col4)` cria grupos para cada combinação de expressões de coluna nas listas a seguir.  

- Col1, col2, col3, col4 
- Col1 col2, col3, NULL
- Col1 col2, NULL, NULL
- Col1, NULL, NULL, NULL
- NULO, nulo, nulo, nulo – este é o total geral

Usando a tabela do exemplo anterior, esse código executa uma operação de GROUP BY ROLLUP em vez de um simples GROUP BY.

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY ROLLUP (Country, Region);
```

O resultado da consulta tem as mesmo agregações como simples GROUP BY sem o pacote cumulativo de atualizações. Além disso, ele cria subtotais para cada valor do país. Por fim, ele fornece um total geral para todas as linhas. O resultado tem esta aparência:

| País | Região | TotalSales |
| :------ | :----- | ---------: |
| Canada | Alberta | 100 |
| Canada | Colúmbia Britânica | 500 |
| Canada | NULL | 600 |
| United States | Montana | 100 |
| United States | NULL | 100 |
| NULL | NULL | 700 |

### <a name="group-by-cube--"></a>AGRUPAR POR (CUBO)  

GROUP BY CUBE cria grupos para todas as combinações possíveis de colunas. GROUP BY CUBE (a, b) os resultados tem grupos de valores exclusivos de (a, b), (b, NULL), (a, NULL) e (nulos, NULL).

Usando a tabela dos exemplos anteriores, esse código executa uma operação de GROUP BY CUBE no país e região. 

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY CUBE (Country, Region);
```

O resultado da consulta tem grupos de valores exclusivos (país, região), (NULL, região), (país, NULL) e (nulos, NULL). Os resultados tem esta aparência:

| País | Região | TotalSales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| NULL | Alberta | 100 |
| Canada | Colúmbia Britânica | 500 |
| NULL | Colúmbia Britânica | 500 |
| United States | Montana | 100 |
| NULL | Montana | 100 |
| NULL | NULL | 700
| Canada | NULL | 600 |
| United States | NULL | 100 |
   
 ### <a name="group-by-grouping-sets--"></a>AGRUPAR POR () DE CONJUNTOS DE AGRUPAMENTO  
 
A opção de conjuntos de AGRUPAMENTOS oferece a capacidade de combinar várias cláusulas GROUP BY em uma cláusula GROUP BY. Os resultados são o equivalente de UNION ALL dos grupos especificados. 

Por exemplo, `GROUP BY ROLLUP (Country, Region)` e `GROUP BY GROUPING SETS ( ROLLUP (Country, Region) )` retornam os mesmos resultados. 

Quando conjuntos de AGRUPAMENTO tem dois ou mais elementos, os resultados são uma união dos elementos. Este exemplo retorna a união dos resultados ROLLUP e CUBE para país e região.

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY GROUPING SETS ( ROLLUP (Country, Region), CUBE (Country, Region) );
```

Os resultados são o mesmo que essa consulta que retorna uma união de duas instruções GROUP BY.

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY ROLLUP (Country, Region)
UNION ALL
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY CUBE (Country, Region)
;
```

SQL não Consolide grupos duplicados gerados para uma lista de conjuntos de AGRUPAMENTOS. Por exemplo, em `GROUP BY ( (), CUBE (Country, Region) )`, ambos os elementos retornarão uma linha para o total geral e ambas as linhas serão listadas nos resultados. 

 ### <a name="group-by-"></a>GROUP BY ()  
Especifica o grupo vazio que gera o total geral. Isso é útil como um dos elementos de um conjunto de AGRUPAMENTO. Por exemplo, esta instrução retorna o total de vendas para cada país e, em seguida, retorna o total geral para todos os países.

```
SELECT Country, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY GROUPING SETS ( Country, () );
```

### <a name="group-by--all--column-expression--n-"></a>GROUP BY [ALL]-expressão de coluna [,... n] 

Aplica-se a: SQL Server e banco de dados SQL do Azure

Observação: Esta sintaxe é fornecida para fins de compatibilidade com versões anteriores. Ele será removido em uma versão futura. Evite usar essa sintaxe em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam essa sintaxe.

Especifica para incluir todos os grupos nos resultados, independentemente de se eles atendem aos critérios de pesquisa na cláusula WHERE. Grupos que não atendem aos critérios de pesquisa tem nulo para a agregação. 

AGRUPAR POR TODOS OS:
- Não há suporte em consultas que acessam tabelas remotas se também houver uma cláusula WHERE na consulta.
- Haverá falha em colunas que têm o atributo FILESTREAM.
  
### <a name="with-distributedagg"></a>COM (DISTRIBUTED_AGG)
Aplica-se a: Azure SQL Data Warehouse e o Parallel Data Warehouse

A dica de consulta DISTRIBUTED_AGG força o sistema de processamento paralelo em massa (MPP) para redistribuir uma tabela em uma coluna específica antes de executar uma agregação. Somente uma coluna na cláusula GROUP BY pode ter uma dica de consulta DISTRIBUTED_AGG. Depois que a consulta for concluída, a tabela redistribuída é descartada. A tabela original não é alterada.  

Observação: A dica de consulta DISTRIBUTED_AGG é fornecida para fins de compatibilidade com versões anteriores do Parallel Data Warehouse e não melhorará o desempenho para a maioria das consultas. Por padrão, MPP já redistribui dados conforme necessário para melhorar o desempenho de agregações. 
  
## <a name="general-remarks"></a>Comentários gerais

### <a name="how-group-by-interacts-with-the-select-statement"></a>Como agrupar por interage com a instrução SELECT
Lista de seleção:
- Agregações de vetor. Se as funções de agregação são incluídas na lista de seleção, GROUP BY calcula um valor resumido para cada grupo. São conhecidas como agregações de vetor. 
- Agregações de DISTINCT. As agregações AVG (DISTINCT *column_name*), contagem (DISTINCT *column_name*) e SUM (DISTINCT *column_name*) têm suporte com ROLLUP, CUBE e GROUPING SETS.
  
Cláusula WHERE:
- SQL remove linhas que não atendem às condições na cláusula WHERE antes de qualquer operação de agrupamento é executada.  
  
Cláusula HAVING:
- SQL usa having cláusula para filtrar grupos no conjunto de resultados. 
  
Cláusula ORDER BY:
- Use a cláusula ORDER BY para ordenar o conjunto de resultados. A cláusula GROUP BY não ordena o conjunto de resultados. 
  
Valores nulos:
- Se uma coluna de agrupamento contiver valores nulos, todos os valores nulos são considerados iguais e eles são coletados em um único grupo.   
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições

Aplica-se a: SQL Server (começando com o 2008) e o Azure SQL Data Warehouse

### <a name="maximum-capacity"></a>Capacidade máxima

Para uma cláusula GROUP BY que usa ROLLUP, CUBE ou GROUPING SETS, o número máximo de expressões é 32. O número máximo de grupos é 4096 (2<sup>12</sup>). Os exemplos a seguir falham porque a cláusula GROUP BY tem mais de 4096 grupos.  
 
-   O exemplo a seguir geram 4097 (2<sup>12</sup> + 1) conjuntos de agrupamentos e falhará.  
  
    ```  
    GROUP BY GROUPING SETS( CUBE(a1, ..., a12), b )  
    ```  
  
-   O exemplo a seguir geram 4097 (2<sup>12</sup> + 1) de grupos e falhará. `CUBE ()` e o conjunto de agrupamentos `()` produzem uma linha de total geral e os conjuntos de agrupamentos duplicados não são eliminados.  
  
    ```  
    GROUP BY GROUPING SETS( CUBE(a1, ..., a12), ())  
    ```  

-   Este exemplo usa a sintaxe compatível com versões anteriores. Ele gera 8192 (2<sup>13</sup>) conjuntos de agrupamentos e falhará.  
  
    ```  
    GROUP BY CUBE (a1, ..., a13)   
    GROUP BY a1, ..., a13 WITH CUBE   
    ```    
    Para compatível com versões anteriores cláusulas GROUP BY que não contêm CUBE ou ROLLUP, o número de grupo por itens é limitado pelos Agrupar por tamanhos de coluna, as colunas de agregação e os valores de agregação envolvidos na consulta. Esse limite tem origem no limite de 8.060 bytes na tabela de trabalho intermediária que é necessária para manter resultados de consulta intermediários. Um máximo de 12 expressões de agrupamento é permitido quando CUBE ou ROLLUP é especificado.

### <a name="support-for-iso-and-ansi-sql-2006-group-by-features"></a>Suporte para os recursos GROUP BY ISO e ANSI SQL-2006

A cláusula GROUP BY dá suporte a todos os recursos GROUP BY que estão incluídos no SQL-2006 padrão com as seguintes exceções de sintaxe:  
  
-   Conjuntos de agrupamentos não são permitidos na cláusula GROUP BY, a menos que sejam parte de uma lista de GROUPING SETS explícita. Por exemplo, `GROUP BY Column1, (Column2, ...ColumnN`) é permitido no padrão, mas não no Transact-SQL.  Oferece suporte a Transact-SQL `GROUP BY C1, GROUPING SETS ((Column2, ...ColumnN))` e `GROUP BY Column1, Column2, ... ColumnN`, que são semanticamente equivalentes. Esses são semanticamente equivalentes ao exemplo `GROUP BY` anterior. Isso é para evitar a possibilidade de que `GROUP BY Column1, (Column2, ...ColumnN`) podem ser interpretados incorretamente como `GROUP BY C1, GROUPING SETS ((Column2, ...ColumnN))`, que não são semanticamente equivalente.  
  
-   Conjuntos de agrupamentos não são permitidos em conjuntos de agrupamentos. Por exemplo, `GROUP BY GROUPING SETS (A1, A2,…An, GROUPING SETS (C1, C2, ...Cn))` é permitido no padrão SQL-2006, mas não no Transact-SQL. Permite que o Transact-SQL `GROUP BY GROUPING SETS( A1, A2,...An, C1, C2, ...Cn )` ou `GROUP BY GROUPING SETS( (A1), (A2), ... (An), (C1), (C2), ... (Cn) )`, que são semanticamente equivalentes ao primeiro exemplo de GROUP BY e têm uma sintaxe mais clara.  
  
-   GROUP BY [ALL/DISTINCT] só é permitido em uma cláusula de GROUP BY simple que contém expressões de coluna. Não é permitido com as construções GROUPING SETS, ROLLUP, CUBE, WITH CUBE ou WITH ROLLUP. ALL é o padrão e está implícito. Só é permitido na sintaxe compatível com versões anteriores.
  
### <a name="comparison-of-supported-group-by-features"></a>Comparação de recursos GROUP BY com suporte  
 A tabela a seguir descreve os recursos GROUP BY que têm suporte com base em versões do SQL e o nível de compatibilidade do banco de dados.  
  
|Recurso|SQL Server Integration Services|Nível de compatibilidade 100 ou superior do SQL Server|Nível de compatibilidade 90 do SQL Server 2008 ou posterior.|  
|-------------|-------------------------------------|--------------------------------------------------|-----------------------------------------------------------|  
|Agregações de DISTINCT|Não há suporte para WITH CUBE ou WITH ROLLUP.|Há suporte para WITH CUBE, WITH ROLLUP, GROUPING SETS, CUBE ou ROLLUP.|Igual ao nível de compatibilidade 100.|  
|Função definida pelo usuário com nome CUBE ou ROLLUP na cláusula GROUP BY|Função definida pelo usuário **dbo. Cube (***arg1***,***... argn***)** ou  **dbo. Rollup (***arg1***,**... *argN***)** em GROUP BY cláusula é permitida.<br /><br /> Por exemplo: `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`|Função definida pelo usuário **dbo. Cube (***arg1***,**... argn**)** ou **dbo. Rollup (**arg1**,***... argn***)** em GROUP BY cláusula não é permitida.<br /><br /> Por exemplo: `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`<br /><br /> A seguinte mensagem de erro é retornada: "sintaxe incorreta próxima a palavra-chave 'cubo' &#124;' pacote cumulativo de atualizações '. "<br /><br /> Para evitar esse problema, substitua `dbo.cube` por `[dbo].[cube]` ou `dbo.rollup` por `[dbo].[rollup]`.<br /><br /> O exemplo a seguir é permitido:`SELECT SUM (x) FROM T  GROUP BY [dbo].[cube](y);`|Função definida pelo usuário **dbo. Cube (***arg1***,***... argn*) ou **dbo. Rollup (** *arg1***,***... argn***)** em GROUP BY cláusula é permitida<br /><br /> Por exemplo: `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`|  
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
  
### <a name="a-use-a-simple-group-by-clause"></a>A. Use uma cláusula GROUP BY simple  
 O exemplo a seguir recupera o total para cada tabela `SalesOrderID` da tabela `SalesOrderDetail`. Este exemplo usa o AdventureWorks.  
  
```  
SELECT SalesOrderID, SUM(LineTotal) AS SubTotal  
FROM Sales.SalesOrderDetail AS sod  
GROUP BY SalesOrderID  
ORDER BY SalesOrderID;  
```  
  
### <a name="b-use-a-group-by-clause-with-multiple-tables"></a>B. Use uma cláusula GROUP BY com várias tabelas  
 O exemplo a seguir recupera o número de funcionários de cada `City` da tabela `Address` unida à tabela `EmployeeAddress`. Este exemplo usa o AdventureWorks. 
  
```  
SELECT a.City, COUNT(bea.AddressID) EmployeeCount  
FROM Person.BusinessEntityAddress AS bea   
    INNER JOIN Person.Address AS a  
        ON bea.AddressID = a.AddressID  
GROUP BY a.City  
ORDER BY a.City;  
```  
  
### <a name="c-use-a-group-by-clause-with-an-expression"></a>C. Usar uma cláusula GROUP BY com uma expressão  
 O exemplo a seguir recupera as vendas totais durante cada ano usando a função `DATEPART`. A mesma expressão deve estar presente na lista `SELECT` e na cláusula `GROUP BY`.  
  
```  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,SUM(TotalDue) AS N'Total Order Amount'  
FROM Sales.SalesOrderHeader  
GROUP BY DATEPART(yyyy,OrderDate)  
ORDER BY DATEPART(yyyy,OrderDate);  
```  
  
### <a name="d-use-a-group-by-clause-with-a-having-clause"></a>D. Use uma cláusula GROUP BY com uma cláusula HAVING  
 O exemplo a seguir usa a cláusula `HAVING` para especificar quais dos grupos gerados na cláusula `GROUP BY` devem ser incluídos no conjunto de resultados.  
  
```  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,SUM(TotalDue) AS N'Total Order Amount'  
FROM Sales.SalesOrderHeader  
GROUP BY DATEPART(yyyy,OrderDate)  
HAVING DATEPART(yyyy,OrderDate) >= N'2003'  
ORDER BY DATEPART(yyyy,OrderDate);  
```  
  
## <a name="examples-sql-data-warehouse-and-parallel-data-warehouse"></a>Exemplos: SQL Data Warehouse e o Parallel Data Warehouse  
  
### <a name="e-basic-use-of-the-group-by-clause"></a>E. Uso básico da cláusula GROUP BY  
 O exemplo a seguir localiza a quantidade total de todas as vendas em cada dia. Uma linha que contém a soma de todas as vendas será retornada para cada dia.  
  
```  
-- Uses AdventureWorksDW  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales FROM FactInternetSales  
GROUP BY OrderDateKey ORDER BY OrderDateKey;  
```  
  
### <a name="f-basic-use-of-the-distributedagg-hint"></a>F. Uso básico da dica de DISTRIBUTED_AGG  
 Este exemplo usa a dica de consulta DISTRIBUTED_AGG para forçar o dispositivo para a tabela em ordem aleatória no `CustomerKey` coluna antes de executar a agregação.  
  
```  
-- Uses AdventureWorksDW  
  
SELECT CustomerKey, SUM(SalesAmount) AS sas  
FROM FactInternetSales  
GROUP BY CustomerKey WITH (DISTRIBUTED_AGG)  
ORDER BY CustomerKey DESC;  
```  
  
### <a name="g-syntax-variations-for-group-by"></a>G. Variações de sintaxe para agrupar por  
 Quando a lista de seleção não tem nenhuma agregação, cada coluna na lista de seleção deve ser incluída na lista GROUP BY. Colunas computadas na lista de seleção podem ser listadas, mas não são necessárias, na lista GROUP BY. Estes são exemplos de instruções SELECT sintaticamente válidos:  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, FirstName FROM DimCustomer GROUP BY LastName, FirstName;  
SELECT NumberCarsOwned FROM DimCustomer GROUP BY YearlyIncome, NumberCarsOwned;  
SELECT (SalesAmount + TaxAmt + Freight) AS TotalCost FROM FactInternetSales GROUP BY SalesAmount, TaxAmt, Freight;  
SELECT SalesAmount, SalesAmount*1.10 SalesTax FROM FactInternetSales GROUP BY SalesAmount;  
SELECT SalesAmount FROM FactInternetSales GROUP BY SalesAmount, SalesAmount*1.10;  
```  
  
### <a name="h-using-a-group-by-with-multiple-group-by-expressions"></a>H. Usando um GROUP BY com várias expressões de GROUP BY  
 O exemplo a seguir agrupa os resultados usando vários `GROUP BY` critérios. Se, dentro de cada `OrderDateKey` grupo, há subgrupos que podem ser diferenciados por `DueDateKey`, um novo agrupamento será definido para o conjunto de resultados.  
  
```  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, DueDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSalesGROUP BY OrderDateKey, DueDateKey   
ORDER BY OrderDateKey;  
```  
  
### <a name="i-using-a-group-by-clause-with-a-having-clause"></a>I. Usando uma cláusula GROUP BY com uma cláusula HAVING  
 O exemplo a seguir usa o `HAVING` cláusula para especificar grupos gerados no `GROUP BY` cláusula deve ser incluída no conjunto de resultados. Somente os grupos com datas de pedido em 2004 ou posteriores serão incluídos nos resultados.  
  
```  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSales  
GROUP BY OrderDateKey   
HAVING OrderDateKey > 20040000   
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>Consulte também  
 [GROUPING_ID &#40; Transact-SQL &#41;](~/t-sql/functions/grouping-id-transact-sql.md)   
 [AGRUPAMENTO &#40; Transact-SQL &#41;](~/t-sql/functions/grouping-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](~/t-sql/queries/select-transact-sql.md)   
 [Cláusula SELECT &#40; Transact-SQL &#41;](~/t-sql/queries/select-clause-transact-sql.md)  
  
  





