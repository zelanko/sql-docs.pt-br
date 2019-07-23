---
title: GROUPING_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GROUPING_ID_TSQL
- GROUPING_ID
dev_langs:
- TSQL
helpviewer_keywords:
- GROUP BY clause, GROUPING_ID
- GROUPING_ID function
ms.assetid: c1050658-b19f-42ee-9a05-ecd6a73b896c
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 13680aea1d34b83d76647d39d0f40b84609b2e8c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910651"
---
# <a name="groupingid-transact-sql"></a>GROUPING_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  É uma função que calcula o nível de agrupamento. GROUPING_ID pode ser usado apenas na lista SELECT \<select> e nas cláusulas HAVING ou ORDER BY quando GROUP BY é especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
GROUPING_ID ( <column_expression>[ ,...n ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 \<column_expression>  
 É uma *column_expression* em uma cláusula [GROUP BY](../../t-sql/queries/select-group-by-transact-sql.md).  
  
## <a name="return-type"></a>Tipo de retorno  
 **int**  
  
## <a name="remarks"></a>Remarks  
 A GROUPING_ID \<column_expression> deve corresponder exatamente à expressão na lista GROUP BY. Por exemplo, se você estiver agrupando por DATEPART (yyyy, \<*column name*>), use GROUPING_ID (DATEPART (yyyy, (yyyy, \<*column name*>)); ou se estiver agrupando por \<*column name*>, use GROUPING_ID (\<*column name*>).  
  
## <a name="comparing-groupingid--to-grouping-"></a>Comparando GROUPING_ID () com GROUPING ()  
 GROUPING_ID (\<column_expression> [ **,** ...*n* ]) insere o equivalente ao retorno de GROUPING (\<column_expression>) para cada coluna em sua lista de colunas em cada linha de saída como uma cadeia de caracteres com números um e zero. GROUPING_ID interpreta a cadeia de caracteres como um número base 2 e retorna o inteiro equivalente. Por exemplo, considere a seguinte instrução: `SELECT a, b, c, SUM(d),``GROUPING_ID(a,b,c)``FROM T GROUP BY <group by list>`. A tabela a seguir mostra os valores de entrada e saída de GROUPING_ID ().  
  
|Colunas agregadas|Entrada de GROUPING_ID (a, b, c) = GROUPING(a) + GROUPING(b) + GROUPING(c)|Saída de GROUPING_ID ()|  
|------------------------|---------------------------------------------------------------------------------------|------------------------------|  
|`a`|`100`|`4`|  
|`b`|`010`|`2`|  
|`c`|`001`|`1`|  
|`ab`|`110`|`6`|  
|`ac`|`101`|`5`|  
|`bc`|`011`|`3`|  
|`abc`|`111`|`7`|  
  
## <a name="technical-definition-of-groupingid-"></a>Definição técnica de GROUPING_ID ()  
 Cada argumento GROUPING_ID deve ser um elemento da lista GROUP BY. GROUPING_ID () retorna um bitmap **integer** cujos N bits inferiores podem ser literais. Um **bit** literal indica que o argumento correspondente não é uma coluna de agrupamento para a linha de saída especificada. O **bit** da ordem mais baixa corresponde ao argumento N e o N-1<sup>º</sup> **bit** de ordem mais baixa corresponde ao argumento 1.  
  
## <a name="groupingid--equivalents"></a>Equivalentes de GROUPING_ID ()  
 Para uma única consulta de agrupamento, GROUPING (\<column_expression>) é equivalente a GROUPING_ID (\<column_expression>) e ambos retornam 0.  
  
 Por exemplo, as instruções seguintes são equivalentes:  
  
 Instrução A:  
  
```  
SELECT GROUPING_ID(A,B)  
FROM T   
GROUP BY CUBE(A,B)   
```  
  
 Instrução B:  
  
```  
SELECT 3 FROM T GROUP BY ()  
UNION ALL  
SELECT 1 FROM T GROUP BY A  
UNION ALL  
SELECT 2 FROM T GROUP BY B  
UNION ALL  
SELECT 0 FROM T GROUP BY A,B  
```  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-groupingid-to-identify-grouping-levels"></a>A. Usando GROUPING_ID para identificar níveis de agrupamento  
 O exemplo a seguir retorna a contagem de funcionários por `Name` e `Title`, `Name,` e o total da empresa no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. `GROUPING_ID()` é usado para criar um valor para cada linha na coluna `Title` que identifica o nível de agregação.  
  
```  
SELECT D.Name  
    ,CASE   
    WHEN GROUPING_ID(D.Name, E.JobTitle) = 0 THEN E.JobTitle  
    WHEN GROUPING_ID(D.Name, E.JobTitle) = 1 THEN N'Total: ' + D.Name   
    WHEN GROUPING_ID(D.Name, E.JobTitle) = 3 THEN N'Company Total:'  
        ELSE N'Unknown'  
    END AS N'Job Title'  
    ,COUNT(E.BusinessEntityID) AS N'Employee Count'  
FROM HumanResources.Employee E  
    INNER JOIN HumanResources.EmployeeDepartmentHistory DH  
        ON E.BusinessEntityID = DH.BusinessEntityID  
    INNER JOIN HumanResources.Department D  
        ON D.DepartmentID = DH.DepartmentID       
WHERE DH.EndDate IS NULL  
    AND D.DepartmentID IN (12,14)  
GROUP BY ROLLUP(D.Name, E.JobTitle);  
```  
  
### <a name="b-using-groupingid-to-filter-a-result-set"></a>B. Usando GROUPING_ID para filtrar um conjunto de resultados  
  
#### <a name="simple-example"></a>Exemplo simples  
 No código a seguir, para retornar somente as linhas com uma contagem de funcionários por título, remova os caracteres de comentário de `HAVING GROUPING_ID(D.Name, E.JobTitle); = 0` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Para retornar somente as linhas com uma contagem de funcionários por departamento, remova os caracteres de comentário de `HAVING GROUPING_ID(D.Name, E.JobTitle) = 1;`.  
  
```  
SELECT D.Name  
    ,E.JobTitle  
    ,GROUPING_ID(D.Name, E.JobTitle) AS 'Grouping Level'  
    ,COUNT(E.BusinessEntityID) AS N'Employee Count'  
FROM HumanResources.Employee AS E  
    INNER JOIN HumanResources.EmployeeDepartmentHistory AS DH  
        ON E.BusinessEntityID = DH.BusinessEntityID  
    INNER JOIN HumanResources.Department AS D  
        ON D.DepartmentID = DH.DepartmentID       
WHERE DH.EndDate IS NULL  
    AND D.DepartmentID IN (12,14)  
GROUP BY ROLLUP(D.Name, E.JobTitle)  
--HAVING GROUPING_ID(D.Name, E.JobTitle) = 0; --All titles  
--HAVING GROUPING_ID(D.Name, E.JobTitle) = 1; --Group by Name;  
```  
  
 Veja o conjunto dos resultados não filtrados:  
  
|Nome|Title|Nível de agrupamento|Contagem de funcionários|Nome|  
|----------|-----------|--------------------|--------------------|----------|  
|Controle de documentos|Especialista de controle|0|2|Controle de documentos|  
|Controle de documentos|Assistente de controle de documentos|0|2|Controle de documentos|  
|Controle de documentos|Gerente de controle de documentos|0|1|Controle de documentos|  
|Controle de documentos|NULL|1|5|Controle de documentos|  
|Instalações e manutenção|Assistente administrativo de instalações|0|1|Instalações e manutenção|  
|Instalações e manutenção|Gerente de instalações|0|1|Instalações e manutenção|  
|Instalações e manutenção|Zelador|0|4|Instalações e manutenção|  
|Instalações e manutenção|Supervisor de manutenção|0|1|Instalações e manutenção|  
|Instalações e manutenção|NULL|1|7|Instalações e manutenção|  
|NULL|NULL|3|12|NULL|  
  
#### <a name="complex-example"></a>Exemplo complexo  
 O exemplo a seguir usa `GROUPING_ID()` para filtrar um conjunto de resultados que contém vários níveis de agrupamento por nível de agrupamento. Um código semelhante pode ser usado para criar uma exibição com vários níveis de agrupamento e um procedimento armazenado que chama a exibição passando um parâmetro para filtrá-la por nível de agrupamento. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
DECLARE @Grouping nvarchar(50);  
DECLARE @GroupingLevel smallint;  
SET @Grouping = N'CountryRegionCode Total';  
  
SELECT @GroupingLevel = (  
    CASE @Grouping  
        WHEN N'Grand Total'             THEN 15  
        WHEN N'SalesPerson Total'       THEN 14  
        WHEN N'Store Total'             THEN 13  
        WHEN N'Store SalesPerson Total' THEN 12  
        WHEN N'CountryRegionCode Total' THEN 11  
        WHEN N'Group Total'             THEN 7  
        ELSE N'Unknown'  
    END);  
  
SELECT   
    T.[Group]  
    ,T.CountryRegionCode  
    ,S.Name AS N'Store'  
    ,(SELECT P.FirstName + ' ' + P.LastName   
        FROM Person.Person AS P   
        WHERE P.BusinessEntityID = H.SalesPersonID)  
        AS N'Sales Person'  
    ,SUM(TotalDue)AS N'TotalSold'  
    ,CAST(GROUPING(T.[Group])AS char(1)) +   
        CAST(GROUPING(T.CountryRegionCode)AS char(1)) +   
        CAST(GROUPING(S.Name)AS char(1)) +   
        CAST(GROUPING(H.SalesPersonID)AS char(1))   
        AS N'GROUPING base-2'  
    ,GROUPING_ID((T.[Group])  
        ,(T.CountryRegionCode),(S.Name),(H.SalesPersonID)  
        ) AS N'GROUPING_ID'  
    ,CASE   
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) = 15 THEN N'Grand Total'  
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) = 14 THEN N'SalesPerson Total'  
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) = 13 THEN N'Store Total'  
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) = 12 THEN N'Store SalesPerson Total'  
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) = 11 THEN N'CountryRegionCode Total'  
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) =  7 THEN N'Group Total'  
        ELSE N'Error'  
        END AS N'Level'  
FROM Sales.Customer AS C  
    INNER JOIN Sales.Store AS S  
        ON C.StoreID  = S.BusinessEntityID   
    INNER JOIN Sales.SalesTerritory AS T  
        ON C.TerritoryID  = T.TerritoryID   
    INNER JOIN Sales.SalesOrderHeader AS H  
        ON C.CustomerID = H.CustomerID  
GROUP BY GROUPING SETS ((S.Name,H.SalesPersonID)  
    ,(H.SalesPersonID),(S.Name)  
    ,(T.[Group]),(T.CountryRegionCode),()  
    )  
HAVING GROUPING_ID(  
    (T.[Group]),(T.CountryRegionCode),(S.Name),(H.SalesPersonID)  
    ) = @GroupingLevel  
ORDER BY   
    GROUPING_ID(S.Name,H.SalesPersonID),GROUPING_ID((T.[Group])  
    ,(T.CountryRegionCode)  
    ,(S.Name)  
    ,(H.SalesPersonID))ASC;  
```  
  
### <a name="c-using-groupingid--with-rollup-and-cube-to-identify-grouping-levels"></a>C. Usando GROUPING_ID () com ROLLUP e CUBE para identificar níveis de agrupamento  
 O código nos exemplos a seguir mostram como usar `GROUPING()` para computar a coluna `Bit Vector(base-2)`. `GROUPING_ID()` é usado para computar a coluna `Integer Equivalent` correspondente. A ordem de colunas na função `GROUPING_ID()` é o oposto da ordem de coluna das colunas que estão concatenadas pela função `GROUPING()`.  
  
 Nesses exemplos, `GROUPING_ID()` é usado para criar um valor para cada linha na coluna `Grouping Level` ao identificar o nível de agrupamento. Os níveis de agrupamento nem sempre são uma lista consecutiva de inteiros que começam com 1 (0, 1, 2, ...*n*).  
  
> [!NOTE]  
>  GROUPING e GROUPING_ID podem ser usados em uma cláusula HAVING para filtrar um conjunto de resultados.  
  
#### <a name="rollup-example"></a>Exemplo de ROLLUP  
 Neste exemplo, todos os níveis de agrupamento não aparecem como no exemplo de CUBE a seguir. Se a ordem das colunas na lista `ROLLUP` for alterada, os valores de nível na coluna `Grouping Level` também terão de ser alterados. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,DATEPART(mm,OrderDate) AS N'Month'  
    ,DATEPART(dd,OrderDate) AS N'Day'  
    ,SUM(TotalDue) AS N'Total Due'  
    ,CAST(GROUPING(DATEPART(dd,OrderDate))AS char(1)) +   
        CAST(GROUPING(DATEPART(mm,OrderDate))AS char(1)) +   
        CAST(GROUPING(DATEPART(yyyy,OrderDate))AS char(1))   
     AS N'Bit Vector(base-2)'  
    ,GROUPING_ID(DATEPART(yyyy,OrderDate)  
        ,DATEPART(mm,OrderDate)  
        ,DATEPART(dd,OrderDate))   
        AS N'Integer Equivalent'  
    ,CASE  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 0 THEN N'Year Month Day'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 1 THEN N'Year Month'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 2 THEN N'not used'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 3 THEN N'Year'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 4 THEN N'not used'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 5 THEN N'not used'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 6 THEN N'not used'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 7 THEN N'Grand Total'  
    ELSE N'Error'  
    END AS N'Grouping Level'  
FROM Sales.SalesOrderHeader  
WHERE DATEPART(yyyy,OrderDate) IN(N'2007',N'2008')  
    AND DATEPART(mm,OrderDate) IN(1,2)  
    AND DATEPART(dd,OrderDate) IN(1,2)  
GROUP BY ROLLUP(DATEPART(yyyy,OrderDate)  
        ,DATEPART(mm,OrderDate)  
        ,DATEPART(dd,OrderDate))  
ORDER BY GROUPING_ID(DATEPART(mm,OrderDate)  
    ,DATEPART(yyyy,OrderDate)  
    ,DATEPART(dd,OrderDate)  
    )  
    ,DATEPART(yyyy,OrderDate)  
    ,DATEPART(mm,OrderDate)  
    ,DATEPART(dd,OrderDate);  
```  
  
 Este é um conjunto de resultados parcial.  
  
|Year|Month|Day|Total devido|Vetor de bit (base 2)|Equivalente inteiro|Nível de agrupamento|  
|----------|-----------|---------|---------------|----------------------------|------------------------|--------------------|  
|2007|1|1|1497452.6066|000|0|Ano Mês Dia|  
|2007|1|2|21772.3494|000|0|Ano Mês Dia|  
|2007|2|1|2705653.5913|000|0|Ano Mês Dia|  
|2007|2|2|21684.4068|000|0|Ano Mês Dia|  
|2008|1|1|1908122.0967|000|0|Ano Mês Dia|  
|2008|1|2|46458.0691|000|0|Ano Mês Dia|  
|2008|2|1|3108771.9729|000|0|Ano Mês Dia|  
|2008|2|2|54598.5488|000|0|Ano Mês Dia|  
|2007|1|NULL|1519224.956|100|1|Ano Mês|  
|2007|2|NULL|2727337.9981|100|1|Ano Mês|  
|2008|1|NULL|1954580.1658|100|1|Ano Mês|  
|2008|2|NULL|3163370.5217|100|1|Ano Mês|  
|2007|NULL|NULL|4246562.9541|110|3|Year|  
|2008|NULL|NULL|5117950.6875|110|3|Year|  
|NULL|NULL|NULL|9364513.6416|111|7|Grand Total|  
  
#### <a name="cube-example"></a>Exemplo de CUBE  
 Neste exemplo, a função `GROUPING_ID()` é usada para criar um valor para cada linha na coluna `Grouping Level` ao identificar o nível de agrupamento.  
  
 Diferentemente de `ROLLUP` no exemplo anterior, `CUBE` gera a saída de todos os níveis de agrupamento. Se a ordem das colunas na lista `CUBE` for alterada, os valores de nível na coluna `Grouping Level` também terão de ser alterados. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]  
  
```  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,DATEPART(mm,OrderDate) AS N'Month'  
    ,DATEPART(dd,OrderDate) AS N'Day'  
    ,SUM(TotalDue) AS N'Total Due'  
    ,CAST(GROUPING(DATEPART(dd,OrderDate))AS char(1)) +   
        CAST(GROUPING(DATEPART(mm,OrderDate))AS char(1)) +   
        CAST(GROUPING(DATEPART(yyyy,OrderDate))AS char(1))   
        AS N'Bit Vector(base-2)'  
    ,GROUPING_ID(DATEPART(yyyy,OrderDate)  
        ,DATEPART(mm,OrderDate)  
        ,DATEPART(dd,OrderDate))   
        AS N'Integer Equivalent'  
    ,CASE  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 0 THEN N'Year Month Day'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 1 THEN N'Year Month'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 2 THEN N'Year Day'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 3 THEN N'Year'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 4 THEN N'Month Day'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 5 THEN N'Month'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 6 THEN N'Day'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 7 THEN N'Grand Total'  
    ELSE N'Error'  
    END AS N'Grouping Level'  
FROM Sales.SalesOrderHeader  
WHERE DATEPART(yyyy,OrderDate) IN(N'2007',N'2008')  
    AND DATEPART(mm,OrderDate) IN(1,2)  
    AND DATEPART(dd,OrderDate) IN(1,2)  
GROUP BY CUBE(DATEPART(yyyy,OrderDate)  
    ,DATEPART(mm,OrderDate)  
    ,DATEPART(dd,OrderDate))  
ORDER BY GROUPING_ID(DATEPART(yyyy,OrderDate)  
    ,DATEPART(mm,OrderDate)  
    ,DATEPART(dd,OrderDate)  
    )  
    ,DATEPART(yyyy,OrderDate)  
    ,DATEPART(mm,OrderDate)  
    ,DATEPART(dd,OrderDate);  
```  
  
 Este é um conjunto de resultados parcial.  
  
|Year|Month|Day|Total devido|Vetor de bit (base 2)|Equivalente inteiro|Nível de agrupamento|  
|----------|-----------|---------|---------------|----------------------------|------------------------|--------------------|  
|2007|1|1|1497452.6066|000|0|Ano Mês Dia|  
|2007|1|2|21772.3494|000|0|Ano Mês Dia|  
|2007|2|1|2705653.5913|000|0|Ano Mês Dia|  
|2007|2|2|21684.4068|000|0|Ano Mês Dia|  
|2008|1|1|1908122.0967|000|0|Ano Mês Dia|  
|2008|1|2|46458.0691|000|0|Ano Mês Dia|  
|2008|2|1|3108771.9729|000|0|Ano Mês Dia|  
|2008|2|2|54598.5488|000|0|Ano Mês Dia|  
|2007|1|NULL|1519224.956|100|1|Ano Mês|  
|2007|2|NULL|2727337.9981|100|1|Ano Mês|  
|2008|1|NULL|1954580.1658|100|1|Ano Mês|  
|2008|2|NULL|3163370.5217|100|1|Ano Mês|  
|2007|NULL|1|4203106.1979|010|2|Ano Dia|  
|2007|NULL|2|43456.7562|010|2|Ano Dia|  
|2008|NULL|1|5016894.0696|010|2|Ano Dia|  
|2008|NULL|2|101056.6179|010|2|Ano Dia|  
|2007|NULL|NULL|4246562.9541|110|3|Year|  
|2008|NULL|NULL|5117950.6875|110|3|Year|  
|NULL|1|1|3405574.7033|001|4|Mês Dia|  
|NULL|1|2|68230.4185|001|4|Mês Dia|  
|NULL|2|1|5814425.5642|001|4|Mês Dia|  
|NULL|2|2|76282.9556|001|4|Mês Dia|  
|NULL|1|NULL|3473805.1218|101|5|Month|  
|NULL|2|NULL|5890708.5198|101|5|Month|  
|NULL|NULL|1|9220000.2675|011|6|Day|  
|NULL|NULL|2|144513.3741|011|6|Day|  
|NULL|NULL|NULL|9364513.6416|111|7|Grand Total|  
  
## <a name="see-also"></a>Consulte Também  
 [GROUPING &#40;Transact-SQL&#41;](../../t-sql/functions/grouping-transact-sql.md)   
 [GROUP BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-group-by-transact-sql.md)  
  
  
