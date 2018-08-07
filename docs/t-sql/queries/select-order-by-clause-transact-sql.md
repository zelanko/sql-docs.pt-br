---
title: Cláusula ORDER BY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ORDER_TSQL
- BY
- ORDER_BY_TSQL
- BY_TSQL
- ORDER
- ORDER BY
dev_langs:
- TSQL
helpviewer_keywords:
- ad-hoc query paging
- OFFSET clause
- SELECT statement [SQL Server], FETCH clause
- clauses [SQL Server], ORDER BY
- SELECT statement [SQL Server], limiting the rows returned
- data [SQL Server], limiting the rows returned
- data [SQL Server], ad-hoc query paging
- sort orders [SQL Server]
- SELECT statement [SQL Server], OFFSET clause
- ORDER BY clause [Transact-SQL]
- LIMIT
- limiting result sets
- SELECT statement [SQL Server], ORDER BY clause
- query paging
- data [SQL Server], sorting
- limiting data returned in a query
- sort orders [SQL Server], ORDER BY clause
- FETCH clause
ms.assetid: bb394abe-cae6-4905-b5c6-8daaded77742
caps.latest.revision: 68
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 831bb6e7000ebc61f0606a0a34760b6478b80f4d
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39456200"
---
# <a name="select---order-by-clause-transact-sql"></a>SELECT – Cláusula ORDER BY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Classifica dados retornados por uma consulta no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use esta cláusula para:  
  
-   Classificar o conjunto de resultados de uma consulta pela lista de colunas especificada e, opcionalmente, limitar as linhas retornadas a um intervalo especificado. A ordem na qual as linhas são retornadas em um conjunto de resultados não é garantida, a menos que uma cláusula ORDER BY seja especificada.  
  
-   Determine a ordem na qual os valores da [função de classificação](../../t-sql/functions/ranking-functions-transact-sql.md) serão aplicados ao conjunto de resultados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
> [!NOTE]  
>  ORDER BY não é compatível com as instruções SELECT/INTO ou CREATE TABLE AS SELECT (CTAS) no [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] nem no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].

## <a name="syntax"></a>Sintaxe  
  
```sql  
-- Syntax for SQL Server and Azure SQL Database  
  
ORDER BY order_by_expression  
    [ COLLATE collation_name ]   
    [ ASC | DESC ]   
    [ ,...n ]   
[ <offset_fetch> ]  
  
<offset_fetch> ::=  
{   
    OFFSET { integer_constant | offset_row_count_expression } { ROW | ROWS }  
    [  
      FETCH { FIRST | NEXT } {integer_constant | fetch_row_count_expression } { ROW | ROWS } ONLY  
    ]  
}  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
[ ORDER BY   
    {  
    order_by_expression   
    [ ASC | DESC ]   
    } [ ,...n ]   
]   
```  
  
## <a name="arguments"></a>Argumentos  
 *order_by_expression*  
 Especifica uma coluna ou expressão na qual o conjunto de resultados da consulta deve ser classificado. Uma coluna de classificação pode ser especificada como um nome ou alias de coluna, ou um inteiro não negativo que representa a posição da coluna na lista de seleção.  
  
 Várias colunas de classificação podem ser especificadas. Os nomes de coluna devem ser exclusivos. A sequência das colunas de classificação na cláusula ORDER BY define a organização do conjunto de resultados classificado. Ou seja, o conjunto de resultados é classificado pela primeira coluna e então essa lista ordenada é classificada pela segunda coluna e assim por diante.  
  
 Os nomes de coluna referenciados na cláusula ORDER BY devem corresponder a uma coluna na lista de seleção ou a uma coluna definida em uma tabela especificada na cláusula FROM sem nenhuma ambiguidade.  
  
 COLLATE *collation_name*  
 Especifica que a operação ORDER BY deve ser executada de acordo com o agrupamento especificado em *collation_name* e não de acordo com o agrupamento da coluna definido na tabela ou na exibição. *collation_name* pode ser um nome de agrupamento do Windows ou um nome de agrupamento SQL. Para obter mais informações, consulte [Suporte a agrupamentos e Unicode](../../relational-databases/collations/collation-and-unicode-support.md). COLLATE é aplicável somente a colunas do tipo **char**, **varchar**, **nchar** e **nvarchar**.  
  
 **ASC** | DESC  
 Define que os valores na coluna especificada devem ser classificados em ordem crescente ou decrescente. ASC classifica do valor mais baixo para o valor mais alto. DESC classifica do valor mais alto para o valor mais baixo. ASC é a ordem de classificação padrão. Valores nulos são tratados como os menores valores possíveis.  
  
 OFFSET { *integer_constant* | *offset_row_count_expression* } { ROW | ROWS }  
 Especifica o número de linhas que devem ser ignoradas antes de começar a retornar linhas da expressão de consulta. O valor pode ser uma expressão ou constante inteira que seja maior que ou igual a zero.  
  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] até o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 *offset_row_count_expression* pode ser uma subconsulta escalar de constante, parâmetro ou variável. Quando uma subconsulta é usada, ela não pode referenciar nenhuma coluna definida no escopo de consulta externa. Ou seja, ela não pode ser correlacionada com a consulta externa.  
  
 ROW e ROWS são sinônimos fornecidos para compatibilidade ANSI.  
  
 Nos planos de execução de consulta, o valor da contagem de linhas de deslocamento é exibido no atributo **Offset** do operador de consulta TOP.  
  
 FETCH { FIRST | NEXT } { *integer_constant* | *fetch_row_count_expression* } { ROW | ROWS } ONLY  
 Especifica o número de linhas que devem ser retornadas depois que a cláusula OFFSET for processada. O valor pode ser uma expressão ou constante inteira que seja maior que ou igual a um.  
  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 *fetch_row_count_expression* pode ser uma subconsulta escalar de constante, parâmetro ou variável. Quando uma subconsulta é usada, ela não pode referenciar nenhuma coluna definida no escopo de consulta externa. Ou seja, ela não pode ser correlacionada com a consulta externa.  
  
 FIRST e NEXT são sinônimos fornecidos para compatibilidade ANSI.  
  
 ROW e ROWS são sinônimos fornecidos para compatibilidade ANSI.  
  
 Nos planos de execução de consulta, o valor da contagem de linhas de deslocamento é exibido no atributo **Rows** ou **Top** do operador de consulta TOP.  
  
## <a name="best-practices"></a>Práticas recomendadas  
 Evite especificar inteiros na cláusula ORDER BY como representações de posição das colunas na lista de seleção. Por exemplo, embora uma instrução como `SELECT ProductID, Name FROM Production.Production ORDER BY 2` seja válida, ela não é entendida por outros com tanta facilidade quanto com a especificação do nome de coluna real. Além disso, as alterações na lista de seleção, como a alteração da ordem das colunas ou a adição de novas colunas, exigirão a modificação da cláusula ORDER BY para evitar resultados inesperados.  
  
 Em uma instrução SELECT TOP (*N*), sempre use uma cláusula ORDER BY. Essa é a única forma de indicar de maneira previsível as linhas que são afetadas por TOP. Para obter mais informações, confira [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md).  
  
## <a name="interoperability"></a>Interoperabilidade  
 Quando usada com uma instrução SELECT...INTO para inserir linhas de outra origem, a cláusula ORDER BY não garante que as linhas sejam inseridas na ordem especificada.  
  
 O uso de OFFSET e FETCH em uma exibição não altera a propriedade updateability da exibição.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 Não há um limite para o número de colunas na cláusula ORDER BY; porém, o tamanho total das colunas especificado em uma cláusula ORDER BY não pode exceder 8.060 bytes.  
  
 As colunas do tipo **ntext**, **text**, **image**, **geography**, **geometry** e  **XML** não podem ser usadas em uma cláusula ORDER BY.  
  
 Nem um inteiro nem uma constante podem ser especificados quando *order_by_expression* aparece em uma função de classificação. Para obter mais informações, consulte [Cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
 Se um nome de tabela tiver um alias na cláusula FROM, apenas o nome do alias poderá ser utilizado para qualificar suas colunas na cláusula ORDER BY.  
  
 Os nomes e aliases de coluna especificados na cláusula ORDER BY deverão ser definidos na lista de seleção, se a instrução SELECT contiver uma das seguintes cláusulas ou dos seguintes operadores:  
  
-   operador UNION  
  
-   operador EXCEPT  
  
-   operador INTERSECT  
  
-   SELECT DISTINCT  
  
 Além disso, quando a instrução incluir um operador UNION, EXCEPT ou INTERSECT, os nomes ou aliases de coluna precisarão ser especificados na lista de seleção da primeira consulta (do lado esquerdo).  
  
 Em uma consulta que usa operadores UNION, EXCEPT ou INTERSECT, ORDER BY é permitida somente ao final da instrução. Essa restrição aplica-se apenas ao especificar UNION, EXCEPT e INTERSECT em uma consulta de nível superior e não em uma subconsulta. Consulte a seção de Exemplos a seguir.  
  
 A cláusula ORDER BY é inválida em exibições, funções embutidas, tabelas derivadas e subconsultas, a menos que as cláusulas TOP ou OFFSET e FETCH também estejam especificadas. Quando ORDER BY é usada nesses objetos, a cláusula é utilizada apenas para determinar as linhas retornadas pela cláusula TOP ou pelas cláusulas OFFSET e FETCH. A cláusula ORDER BY não garante resultados ordenados quando essas construções são consultadas, a menos que ORDER BY também seja especificada na própria consulta.  
  
 Não há suporte para OFFSET e FETCH exibições indexadas ou em uma exibição definida usando a cláusula de CHECK OPTION.  
  
 OFFSET e FETCH podem ser usadas em qualquer consulta que permita TOP e ORDER BY, com as seguintes limitações:  
  
-   A cláusula OVER não dá suporte a OFFSET e FETCH.  
  
-   Não é possível especificar OFFSET e FETCH diretamente em instruções INSERT, UPDATE, MERGE e DELETE, mas elas podem ser especificadas em uma subconsulta definida nessas instruções. Por exemplo, na instrução INSERT INTO SELECT, OFFSET e FETCH podem ser especificadas na instrução SELECT.  
  
-   Em uma consulta que use operadores UNION, EXCEPT ou INTERSECT, OFFSET e FETCH podem ser especificadas somente na consulta final que define a ordem dos resultados da consulta.  
  
-   Não é possível combinar TOP com OFFSET e FETCH na mesma expressão de consulta (no mesmo escopo de consulta).  
  
## <a name="using-offset-and-fetch-to-limit-the-rows-returned"></a>Usando OFFSET e FETCH para limitar as linhas retornadas  
 É recomendável usar as cláusulas OFFSET e FETCH em vez da cláusula TOP para implementar uma solução de paginação de consulta e limitar o número de linhas enviadas a um aplicativo cliente.  
  
 O uso de OFFSET e FETCH como solução de paginação exige a execução da consulta uma vez para cada "página" de dados retornados para o aplicativo cliente. Por exemplo, para retornar os resultados de uma consulta em incrementos de 10 linhas, você deve executar a consulta uma vez para retornar as linhas 1 a 10, depois executar a consulta novamente para retornar as linhas 11 a 20 e assim por diante. Cada consulta é independente e elas não são relacionadas entre si. Isso significa que, diferentemente de usar um cursor no qual a consulta é executada uma vez e o estado é mantido no servidor, o aplicativo cliente é responsável para controlar o estado. Para obter resultados estáveis entre solicitações de consulta que usam OFFSET e FETCH, as seguintes condições devem ser atendidas:  
  
1.  Os dados subjacentes que são usados pela consulta não devem ser alterados. Ou seja, as linhas afetadas pela consulta não são atualizadas ou todas as solicitações de páginas da consulta são executadas em uma única transação usando isolamento de transação serializável ou de instantâneo. Para obter mais informações sobre esses níveis de isolamento de transação, confira [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
2.  A cláusula ORDER BY contém uma coluna ou combinação de colunas cuja exclusividade é garantida.  
  
 Consulte o exemplo "Executando várias consultas em uma única transação" na seção de Exemplos posteriormente neste tópico.  
  
 Se planos de execução consistentes forem importantes na sua solução de paginação, considere o uso da dica de consulta OPTIMIZE FOR para os parâmetros OFFSET e FETCH. Consulte "Especificado expressões para valores de OFFSET e FETCH" na seção de Exemplos posteriormente neste tópico. Para obter mais informações sobre OPTIMIZE FOR, confira [Dicas de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
## <a name="examples"></a>Exemplos  
  
|Categoria|Elementos de sintaxe em destaque|  
|--------------|------------------------------|  
|[Sintaxe básica](#BasicSyntax)|ORDER BY|  
|[Especificando a ordem crescente e decrescente](#SortOrder)|DESC • ASC|  
|[Especificando um agrupamento](#Collation)|COLLATE|  
|[Especificando uma ordem condicional](#Case)|expressão CASE|  
|[Usando ORDER BY em uma função de classificação](#Rank)|Funções de classificação|  
|[Limitando o número de linhas retornadas](#Offset)|OFFSET • FETCH|  
|[Usando ORDER BY com UNION, EXCEPT e INTERSECT](#Union)|UNION|  
  
###  <a name="BasicSyntax"></a> Sintaxe básica  
 Os exemplos nesta seção demonstram a funcionalidade básica da cláusula ORDER BY usando a sintaxe mínima necessária.  
  
#### <a name="a-specifying-a-single-column-defined-in-the-select-list"></a>A. Especificando uma única coluna definida na lista de seleção  
 O exemplo a seguir classifica o conjunto de resultados pela coluna numérica `ProductID`. Como não foi especificada nenhuma ordem de classificação específica, o padrão (ordem crescente) é usado.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name FROM Production.Product  
WHERE Name LIKE 'Lock Washer%'  
ORDER BY ProductID;  
```  
  
#### <a name="b-specifying-a-column-that-is-not-defined-in-the-select-list"></a>B. Especificando uma única coluna não definida na lista de seleção  
 O exemplo a seguir classifica o conjunto de resultados por uma coluna que não está incluída na lista de seleção, mas que foi definida na tabela especificada na cláusula FROM.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name, Color  
FROM Production.Product  
ORDER BY ListPrice;  
  
```  
  
#### <a name="c-specifying-an-alias-as-the-sort-column"></a>C. Especificando um alias como a coluna de classificação  
 O exemplo a seguir especifica o alias de coluna `SchemaName` como a coluna da ordem de classificação.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT name, SCHEMA_NAME(schema_id) AS SchemaName  
FROM sys.objects  
WHERE type = 'U'  
ORDER BY SchemaName;  
  
```  
  
#### <a name="d-specifying-an-expression-as-the-sort-column"></a>D. Especificando uma expressão como a coluna de classificação  
 O exemplo a seguir usa uma expressão como a coluna de classificação. A expressão é definida usando a função DATEPART para classificar o conjunto de resultados pelo ano no qual os funcionários foram contratados.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT BusinessEntityID, JobTitle, HireDate  
FROM HumanResources.Employee  
ORDER BY DATEPART(year, HireDate);  
  
```  
  
###  <a name="SortOrder"></a> Especificando a ordem de classificação crescente e decrescente  
  
#### <a name="a-specifying-a-descending-order"></a>A. Especificando uma ordem decrescente  
 O exemplo a seguir classifica o conjunto de resultados pela coluna numérica `ProductID` na ordem decrescente.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name FROM Production.Product  
WHERE Name LIKE 'Lock Washer%'  
ORDER BY ProductID DESC;  
  
```  
  
#### <a name="b-specifying-an-ascending-order"></a>B. Especificando uma ordem crescente  
 O exemplo a seguir classifica o conjunto de resultados pela coluna `Name` na ordem crescente. Os caracteres são classificados em ordem alfabética e não em ordem numérica. Ou seja, 10 é tem uma classificação anterior a 2.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name FROM Production.Product  
WHERE Name LIKE 'Lock Washer%'  
ORDER BY Name ASC ;  
  
```  
  
#### <a name="c-specifying-both-ascending-and-descending-order"></a>C. Especificando as ordens crescente e decrescente  
 O exemplo a seguir classifica o conjunto de resultados por duas colunas. O conjunto de resultados da consulta é classificado primeiro na ordem crescente pela coluna `FirstName` e, em seguida, na ordem decrescente pela coluna `LastName`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT LastName, FirstName FROM Person.Person  
WHERE LastName LIKE 'R%'  
ORDER BY FirstName ASC, LastName DESC ;  
  
```  
  
###  <a name="Collation"></a> Especificando um agrupamento  
 O exemplo a seguir mostra como a especificação de um agrupamento na cláusula ORDER BY pode alterar a ordem na qual os resultados da consulta são retornados. É criada uma tabela que contém uma coluna definida usando um agrupamento sem diferenciação de maiúsculas e minúsculas, nem de acentos. Os valores são inseridos com várias diferenças de maiúsculas e minúsculas e de acentos. Como não foi especificado um agrupamento na cláusula ORDER BY, a primeira consulta usa o agrupamento da coluna ao classificar os valores. Na segunda consulta, um agrupamento com diferenciação de maiúsculas e minúsculas e de acentos é especificado na cláusula ORDER BY, o que altera a ordem na qual as linhas são retornadas.  
  
```  
USE tempdb;  
GO  
CREATE TABLE #t1 (name nvarchar(15) COLLATE Latin1_General_CI_AI)  
GO  
INSERT INTO #t1 VALUES(N'Sánchez'),(N'Sanchez'),(N'sánchez'),(N'sanchez');  
  
-- This query uses the collation specified for the column 'name' for sorting.  
SELECT name  
FROM #t1  
ORDER BY name;  
-- This query uses the collation specified in the ORDER BY clause for sorting.  
SELECT name  
FROM #t1  
ORDER BY name COLLATE Latin1_General_CS_AS;  
  
```  
  
###  <a name="Case"></a> Especificando uma ordem condicional  
 O exemplo a seguir usa a expressão CASE em uma cláusula ORDER BY para determinar condicionalmente a ordem de classificação das linhas com base em um determinado valor de coluna. No primeiro exemplo, é avaliado o valor da coluna `SalariedFlag` da tabela `HumanResources.Employee`. Funcionários que têm o `SalariedFlag` definido como 1 são retornados pelo `BusinessEntityID` em ordem decrescente. Funcionários que têm o `SalariedFlag` definido como 0 são retornados pelo `BusinessEntityID` em ordem crescente. No segundo exemplo, o conjunto de resultados será ordenado pela coluna `TerritoryName` quando a coluna `CountryRegionName` for igual a 'United States' e por `CountryRegionName` para todas as outras linhas.  
  
```  
SELECT BusinessEntityID, SalariedFlag  
FROM HumanResources.Employee  
ORDER BY CASE SalariedFlag WHEN 1 THEN BusinessEntityID END DESC  
        ,CASE WHEN SalariedFlag = 0 THEN BusinessEntityID END;  
GO  
  
```  
  
```  
SELECT BusinessEntityID, LastName, TerritoryName, CountryRegionName  
FROM Sales.vSalesPerson  
WHERE TerritoryName IS NOT NULL  
ORDER BY CASE CountryRegionName WHEN 'United States' THEN TerritoryName  
         ELSE CountryRegionName END;  
  
```  
  
###  <a name="Rank"></a> Usando ORDER BY em uma função de classificação  
 O exemplo as seguir usa a cláusula ORDER BY nas funções de classificação ROW_NUMBER, RANK, DENSE_RANK e NTILE.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName  
    ,ROW_NUMBER() OVER (ORDER BY a.PostalCode) AS "Row Number"  
    ,RANK() OVER (ORDER BY a.PostalCode) AS "Rank"  
    ,DENSE_RANK() OVER (ORDER BY a.PostalCode) AS "Dense Rank"  
    ,NTILE(4) OVER (ORDER BY a.PostalCode) AS "Quartile"  
    ,s.SalesYTD, a.PostalCode  
FROM Sales.SalesPerson AS s   
    INNER JOIN Person.Person AS p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address AS a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL AND SalesYTD <> 0;  
  
```  
  
###  <a name="Offset"></a> Limitando o número de linhas retornadas  
 Os exemplos as seguir usam OFFSET e FETCH para limitar o número de linhas retornadas por uma consulta.  
  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
#### <a name="a-specifying-integer-constants-for-offset-and-fetch-values"></a>A. Especificando constantes inteiras para valores de OFFSET e FETCH  
 O exemplo a seguir especifica uma constante inteira como o valor das cláusulas OFFSET e FETCH. A primeira consulta retorna todas as linhas classificadas pela coluna `DepartmentID`. Compare os resultados retornados por essa consulta com os resultados das duas consultas seguintes. A próxima consulta usa a cláusula `OFFSET 5 ROWS` para ignorar as cinco primeiras linhas e retornar todas as linhas restantes. A consulta final usa a cláusula `OFFSET 0 ROWS` para iniciar com a primeira linha e depois usa `FETCH NEXT 10 ROWS ONLY` para limitar as linhas retornadas a 10 linhas do conjunto de resultados classificado.  
  
```  
USE AdventureWorks2012;  
GO  
-- Return all rows sorted by the column DepartmentID.  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID;  
  
-- Skip the first 5 rows from the sorted result set and return all remaining rows.  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID OFFSET 5 ROWS;  
  
-- Skip 0 rows and return only the first 10 rows from the sorted result set.  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID   
    OFFSET 0 ROWS  
    FETCH NEXT 10 ROWS ONLY;  
  
```  
  
#### <a name="b-specifying-variables-for-offset-and-fetch-values"></a>B. Especificando variáveis para valores de OFFSET e FETCH  
 O exemplo a seguir declara as variáveis `@StartingRowNumber` e `@FetchRows`, e especifica essas variáveis nas cláusulas OFFSET e FETCH.  
  
```  
USE AdventureWorks2012;  
GO  
-- Specifying variables for OFFSET and FETCH values    
DECLARE @StartingRowNumber tinyint = 1  
      , @FetchRows tinyint = 8;  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID ASC   
    OFFSET @StartingRowNumber ROWS   
    FETCH NEXT @FetchRows ROWS ONLY;  
  
```  
  
#### <a name="c-specifying-expressions-for-offset-and-fetch-values"></a>C. Especificando expressões para valores de OFFSET e FETCH  
 O exemplo a seguir usa a expressão `@StartingRowNumber - 1` para especificar o valor de OFFSET e a expressão `@EndingRowNumber - @StartingRowNumber + 1` para especificar o valor de FETCH. Além disso, é especificada a dica de consulta, OPTIMIZE FOR. Essa dica pode ser usada para fornecer um valor específico para uma variável local quando a consulta é compilada e otimizada. O valor é usado somente durante a otimização da consulta e não durante sua execução. Para obter mais informações, veja [Dicas de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
```  
USE AdventureWorks2012;  
GO  
  
-- Specifying expressions for OFFSET and FETCH values      
DECLARE @StartingRowNumber tinyint = 1  
      , @EndingRowNumber tinyint = 8;  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID ASC   
    OFFSET @StartingRowNumber - 1 ROWS   
    FETCH NEXT @EndingRowNumber - @StartingRowNumber + 1 ROWS ONLY  
OPTION ( OPTIMIZE FOR (@StartingRowNumber = 1, @EndingRowNumber = 20) );  
  
```  
  
#### <a name="d-specifying-a-constant-scalar-subquery-for-offset-and-fetch-values"></a>D. Especificando uma subconsulta escalar de constante para valores de OFFSET e FETCH  
 O exemplo a seguir usa uma subconsulta escalar de constante para definir o valor para a cláusula FETCH. A subconsulta retorna um único valor da coluna `PageSize` da tabela `dbo.AppSettings`.  
  
```  
-- Specifying a constant scalar subquery  
USE AdventureWorks2012;  
GO  
CREATE TABLE dbo.AppSettings (AppSettingID int NOT NULL, PageSize int NOT NULL);  
GO  
INSERT INTO dbo.AppSettings VALUES(1, 10);  
GO  
DECLARE @StartingRowNumber tinyint = 1;  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID ASC   
    OFFSET @StartingRowNumber ROWS   
    FETCH NEXT (SELECT PageSize FROM dbo.AppSettings WHERE AppSettingID = 1) ROWS ONLY;  
  
```  
  
#### <a name="e-running-multiple-queries-in-a-single-transaction"></a>E. Executando várias consultas em uma única transação  
 O exemplo a seguir mostra um método de implementação de uma solução de paginação que assegura que sejam retornados resultados estáveis em todas as solicitações da consulta. A consulta é executada em uma única transação usando o nível de isolamento do instantâneo e a coluna especificada na cláusula ORDER BY assegura a exclusividade da coluna.  
  
```  
USE AdventureWorks2012;  
GO  
  
-- Ensure the database can support the snapshot isolation level set for the query.  
IF (SELECT snapshot_isolation_state FROM sys.databases WHERE name = N'AdventureWorks2012') = 0  
    ALTER DATABASE AdventureWorks2012 SET ALLOW_SNAPSHOT_ISOLATION ON;  
GO  
  
-- Set the transaction isolation level  to SNAPSHOT for this query.  
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
GO  
  
-- Beging the transaction  
BEGIN TRANSACTION;  
GO  
-- Declare and set the variables for the OFFSET and FETCH values.  
DECLARE @StartingRowNumber int = 1  
      , @RowCountPerPage int = 3;  
  
-- Create the condition to stop the transaction after all rows have been returned.  
WHILE (SELECT COUNT(*) FROM HumanResources.Department) >= @StartingRowNumber  
BEGIN  
  
-- Run the query until the stop condition is met.  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID ASC   
    OFFSET @StartingRowNumber - 1 ROWS   
    FETCH NEXT @RowCountPerPage ROWS ONLY;  
  
-- Increment @StartingRowNumber value.  
SET @StartingRowNumber = @StartingRowNumber + @RowCountPerPage;  
CONTINUE  
END;  
GO  
COMMIT TRANSACTION;  
GO  
  
```  
  
###  <a name="Union"></a> Usando ORDER BY com UNION, EXCEPT e INTERSECT  
 Quando uma consulta usa os operadores UNION, EXCEPT ou INTERSECT, a cláusula ORDER BY deve ser especificada no final da instrução e os resultados das consultas combinadas são classificados. O exemplo as seguir retorna todos os produtos que são vermelhos ou amarelos e classifica essa lista combinada pela coluna `ListPrice`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Name, Color, ListPrice  
FROM Production.Product  
WHERE Color = 'Red'  
-- ORDER BY cannot be specified here.  
UNION ALL  
SELECT Name, Color, ListPrice  
FROM Production.Product  
WHERE Color = 'Yellow'  
ORDER BY ListPrice ASC;  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir demonstra a ordenação de um conjunto de resultados pela coluna numérica `EmployeeKey` em ordem crescente.  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, FirstName, LastName FROM DimEmployee  
WHERE LastName LIKE 'A%'  
ORDER BY EmployeeKey;  
```  
  
 O exemplo a seguir classifica um conjunto de resultados pela coluna numérica `EmployeeKey` em ordem decrescente.  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, FirstName, LastName FROM DimEmployee  
WHERE LastName LIKE 'A%'  
ORDER BY EmployeeKey DESC;  
```  
  
 O exemplo a seguir classifica um conjunto de resultados pela coluna `LastName`.  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, FirstName, LastName FROM DimEmployee  
WHERE LastName LIKE 'A%'  
ORDER BY LastName;  
```  
  
 O exemplo a seguir ordena por duas colunas. Esta consulta classifica primeiro em ordem crescente pela coluna `FirstName` e, em seguida, classifica os valores comuns de `FirstName` em ordem decrescente pela coluna `LastName`.  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, FirstName, LastName FROM DimEmployee  
WHERE LastName LIKE 'A%'  
ORDER BY LastName, FirstName;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [Funções de classificação &#40;Transact-SQL&#41;](../../t-sql/functions/ranking-functions-transact-sql.md)   
 [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md)   
 [Dicas de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)   
 [EXCEPT e INTERSECT &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)   
 [UNION &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-operators-union-transact-sql.md)   
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)  
  
  

