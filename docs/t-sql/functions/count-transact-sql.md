---
title: COUNT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COUNT_TSQL
- COUNT
dev_langs:
- TSQL
helpviewer_keywords:
- totals [SQL Server], COUNT function
- totals [SQL Server]
- counting items in group
- groups [SQL Server], number of items in
- number of group items
- COUNT function [Transact-SQL]
ms.assetid: 28d39da6-bc2e-46c7-858c-b1721c938830
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ddd5d9584f71e8a6b1ae9686203463b1eb77f47e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65944679"
---
# <a name="count-transact-sql"></a>COUNT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Essa função retorna o número de itens encontrados em um grupo. `COUNT` funciona como a função [COUNT_BIG](../../t-sql/functions/count-big-transact-sql.md). Essas funções são diferentes apenas nos tipos de dados de seus valores de retorno. `COUNT` sempre retorna um valor do tipo de dados **int**. `COUNT_BIG` sempre retorna um valor do tipo de dados **bigint**.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql

-- Aggregation Function Syntax  
COUNT ( { [ [ ALL | DISTINCT ] expression ] | * } )  

-- Analytic Function Syntax  
COUNT ( [ ALL ]  { expression | * } ) OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>Argumentos  
**ALL**  
Aplica a função de agregação a todos os valores. ALL funciona como o padrão.
  
DISTINCT  
Especifica que `COUNT` retorna o número de valores não nulos exclusivos.
  
*expressão*  
Uma [expression](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer tipo, exceto **image**, **ntext** ou **text**. Observe que `COUNT` não oferece suporte a funções de agregação ou subconsultas em uma expressão.
  
\*  
Especifica que `COUNT` deve contar todas as linhas para determinar a contagem total de linhas da tabela para retornar. `COUNT(*)` não usa nenhum parâmetro e não oferece suporte ao uso de DISTINCT. `COUNT(*)` não exige um parâmetro *expression* porque, por definição, não usa informações sobre nenhuma coluna específica. `COUNT(*)` retorna o número de linhas em uma tabela especificada e preserva linhas duplicatas. Ele conta cada linha separadamente. Isso inclui linhas que contêm valores nulos.
  
OVER **(** [ *partition_by_clause* ] [ *order_by_clause* ] [ *ROW_or_RANGE_clause* ] **)**  
A *partition_by_clause* divide o conjunto de resultados produzido pela cláusula `FROM` em partições às quais a função `COUNT` é aplicada. Se não for especificado, a função tratará todas as linhas do conjunto de resultados da consulta como um único grupo. A *order_by_clause* determina a ordem lógica da operação. Veja [Cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md) para saber mais. 

## <a name="return-types"></a>Tipos de retorno
 **int**  
  
## <a name="remarks"></a>Remarks  
COUNT(\*) retorna o número de itens de um grupo. Isso inclui valores NULL e duplicatas.
  
COUNT(ALL *expression*) avalia a *expression* de cada linha em um grupo e retorna o número de valores não nulos.
  
COUNT(DISTINCT *expression*) avalia a *expression* de cada linha em um grupo e retorna o número de valores não nulos exclusivos.
  
Para retornar valores superiores a 2^31-1, `COUNT` retornará um erro. Nesses casos, use `COUNT_BIG` em vez disso.
  
`COUNT` é uma função determinística quando usada ***sem*** as cláusulas OVER e ORDER BY. É não determinística quando especificada ***com*** as cláusulas OVER e ORDER BY. Veja [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md) para saber mais.
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-count-and-distinct"></a>A. Usando COUNT e DISTINCT  
Este exemplo retorna o número de cargos diferentes que um funcionário [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] pode ter.
  
```sql
SELECT COUNT(DISTINCT Title)  
FROM HumanResources.Employee;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
67  
  
(1 row(s) affected)
```
  
### <a name="b-using-count"></a>B. Como usar COUNT(\*)  
Este exemplo retorna o número total de funcionários [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)].
  
```sql
SELECT COUNT(*)  
FROM HumanResources.Employee;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
290  
  
(1 row(s) affected)
```
  
### <a name="c-using-count-with-other-aggregates"></a>C. Como usar COUNT(\*) com outras agregações  
Este exemplo mostra que `COUNT(*)` funciona com outras funções de agregação na lista `SELECT`. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].
  
```sql
SELECT COUNT(*), AVG(Bonus)  
FROM Sales.SalesPerson  
WHERE SalesQuota > 25000;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
----------- ---------------------
14            3472.1428
  
(1 row(s) affected)
```
  
### <a name="d-using-the-over-clause"></a>D. Usando a cláusula OVER  
Este exemplo usa as funções `MIN`, `MAX`, `AVG` e `COUNT` com a cláusula `OVER`, para retornar valores agregados para cada departamento no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] da tabela `HumanResources.Department`.
  
```sql
SELECT DISTINCT Name  
       , MIN(Rate) OVER (PARTITION BY edh.DepartmentID) AS MinSalary  
       , MAX(Rate) OVER (PARTITION BY edh.DepartmentID) AS MaxSalary  
       , AVG(Rate) OVER (PARTITION BY edh.DepartmentID) AS AvgSalary  
       ,COUNT(edh.BusinessEntityID) OVER (PARTITION BY edh.DepartmentID) AS EmployeesPerDept  
FROM HumanResources.EmployeePayHistory AS eph  
JOIN HumanResources.EmployeeDepartmentHistory AS edh  
     ON eph.BusinessEntityID = edh.BusinessEntityID  
JOIN HumanResources.Department AS d  
ON d.DepartmentID = edh.DepartmentID
WHERE edh.EndDate IS NULL  
ORDER BY Name;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Name                          MinSalary             MaxSalary             AvgSalary             EmployeesPerDept  
----------------------------- --------------------- --------------------- --------------------- ----------------  
Document Control              10.25                 17.7885               14.3884               5  
Engineering                   32.6923               63.4615               40.1442               6  
Executive                     39.06                 125.50                68.3034               4  
Facilities and Maintenance    9.25                  24.0385               13.0316               7  
Finance                       13.4615               43.2692               23.935                10  
Human Resources               13.9423               27.1394               18.0248               6  
Information Services          27.4038               50.4808               34.1586               10  
Marketing                     13.4615               37.50                 18.4318               11  
Production                    6.50                  84.1346               13.5537               195  
Production Control            8.62                  24.5192               16.7746               8  
Purchasing                    9.86                  30.00                 18.0202               14  
Quality Assurance             10.5769               28.8462               15.4647               6  
Research and Development      40.8654               50.4808               43.6731               4  
Sales                         23.0769               72.1154               29.9719               18  
Shipping and Receiving        9.00                  19.2308               10.8718               6  
Tool Design                   8.62                  29.8462               23.5054               6  
  
(16 row(s) affected)
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-count-and-distinct"></a>E. Usando COUNT e DISTINCT  
Este exemplo retorna o número de cargos diferentes que um funcionário de uma empresa específica pode ter.
  
```sql
USE ssawPDW;  
  
SELECT COUNT(DISTINCT Title)  
FROM dbo.DimEmployee;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
67
```  
  
### <a name="f-using-count"></a>F. Como usar COUNT(\*)  
Este exemplo retorna o número total de linhas na tabela `dbo.DimEmployee`.
  
```sql
USE ssawPDW;  
  
SELECT COUNT(*)  
FROM dbo.DimEmployee;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-------------
296
```  
  
### <a name="g-using-count-with-other-aggregates"></a>G. Como usar COUNT(\*) com outras agregações  
Este exemplo combina `COUNT(*)` com outras funções de agregação na lista `SELECT`. Ele retorna o número de representantes de vendas com uma cota de vendas anual maior que US$ 500.000 e a cota de vendas média desses representantes de vendas.
  
```sql
USE ssawPDW;  
  
SELECT COUNT(EmployeeKey) AS TotalCount, AVG(SalesAmountQuota) AS [Average Sales Quota]  
FROM dbo.FactSalesQuota  
WHERE SalesAmountQuota > 500000 AND CalendarYear = 2001;  
  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
TotalCount  Average Sales Quota
----------  -------------------
10          683800.0000
```
  
### <a name="h-using-count-with-having"></a>H. Usando COUNT com HAVING  
Este exemplo usa `COUNT` com a cláusula `HAVING` para retornar os departamentos de uma empresa, cada qual com mais de 15 funcionários.
  
```sql
USE ssawPDW;  
  
SELECT DepartmentName,   
       COUNT(EmployeeKey)AS EmployeesInDept  
FROM dbo.DimEmployee  
GROUP BY DepartmentName  
HAVING COUNT(EmployeeKey) > 15;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
DepartmentName  EmployeesInDept
--------------  ---------------
Sales           18
Production      179
```
  
### <a name="i-using-count-with-over"></a>I. Usando COUNT com OVER  
Este exemplo a seguir usa `COUNT` com a cláusula `OVER` para retornar o número de produtos que estão contidos em cada uma das ordens de venda especificadas.
  
```sql
USE ssawPDW;  
  
SELECT DISTINCT COUNT(ProductKey) OVER(PARTITION BY SalesOrderNumber) AS ProductCount  
    ,SalesOrderNumber  
FROM dbo.FactInternetSales  
WHERE SalesOrderNumber IN (N'SO53115',N'SO55981');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
ProductCount   SalesOrderID`
------------   -----------------
3              SO53115
1              SO55981
```
  
## <a name="see-also"></a>Confira também
[Funções de agregação &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[COUNT_BIG &#40;Transact-SQL&#41;](../../t-sql/functions/count-big-transact-sql.md)  
[Cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  


