---
title: MIN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- MIN
- MIN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MIN function [Transact-SQL]
- minimum values [SQL Server]
- values [SQL Server], minimum
ms.assetid: 56cf6ec5-34f5-47e3-a402-7129039d4429
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7ebdb67cb942413d94837822061877bd7fe7eadd
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828722"
---
# <a name="min-transact-sql"></a>MIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna o valor mínimo na expressão. Pode ser seguido pela [cláusula OVER](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
  
-- Aggregation Function Syntax  
MIN ( [ ALL | DISTINCT ] expression )  
  
-- Analytic Function Syntax   
MIN ( [ ALL ] expression ) OVER ( [ <partition_by_clause> ] [ <order_by_clause> ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 **ALL**  
 Aplica a função de agregação a todos os valores. ALL é o padrão.  
  
 DISTINTO  
 Especifica que cada valor exclusivo é considerado. DISTINCT não é significativo com MIN e está disponível somente para compatibilidade com ISO.  
  
 *expressão*  
 É uma constante, nome de coluna ou função e qualquer combinação de operadores aritméticos, bit a bit e de cadeia de caracteres. MIN pode ser usado com colunas **numeric**, **char**, **varchar**, **uniqueidentifier** ou **datetime**, mas não com colunas **bit**. Funções de agregação e subconsultas não são permitidas.  
  
 Para obter mais informações, veja [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 OVER **(** [ _partition\_by\_clause_ ] _order\_by\_clause_ **)**  
 *partition_by_clause* divide o conjunto de resultados produzido pela cláusula FROM em partições às quais a função é aplicada. Se não for especificado, a função tratará todas as linhas do conjunto de resultados da consulta como um único grupo. *order_by_clause* determina a ordem lógica na qual a operação é executada. *order_by_clause* é obrigatório. Para obter mais informações, consulte [Cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna um valor igual a *expression*.  
  
## <a name="remarks"></a>Comentários  
 MIN ignora quaisquer valores nulos.  
  
 Com colunas de dados de caractere, MIN localiza o valor mais baixo na sequência de classificação.  
  
 MIN é uma função determinística quando usada sem as cláusulas OVER e ORDER BY. É não determinística quando especificada com as cláusulas OVER e ORDER BY. Para obter mais informações, veja [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-simple-example"></a>a. Exemplo simples  
 O exemplo a seguir retorna a taxa de imposto mais baixa (mínima). O exemplo usa o banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]  
  
```  
SELECT MIN(TaxRate)  
FROM Sales.SalesTaxRate;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 -------------------
  
 5.00
  
 (1 row(s) affected)
 ```  
  
### <a name="b-using-the-over-clause"></a>B. Usando a cláusula OVER  
 O exemplo a seguir usa as funções MIN, MAX, AVG e COUNT com a cláusula OVER para fornecer valores agregados para cada departamento na tabela `HumanResources.Department` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
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
  
```  
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
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-min"></a>C. Usando MIN  
 O exemplo a seguir usa a função de agregação MIN para retornar o preço do produto menos caro (mínimo) em um conjunto especificado de ordens de venda.  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT MIN(UnitPrice)  
FROM dbo.FactResellerSales   
WHERE SalesOrderNumber IN (N'SO43659', N'SO43660', N'SO43664');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ------  
 5.1865
 ```  
  
### <a name="d-using-min-with-over"></a>D. Usando MIN com OVER  
 Os exemplos a seguir usam a função analítica MIN OVER() para retornar o preço do produto menos caro em cada ordem de vendas. O conjunto de resultados é particionado pela coluna `SalesOrderID`.  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT MIN(UnitPrice) OVER(PARTITION BY SalesOrderNumber) AS LeastExpensiveProduct,  
       SalesOrderNumber  
FROM dbo.FactResellerSales    
WHERE SalesOrderNumber IN (N'SO43659', N'SO43660', N'SO43664')  
ORDER BY SalesOrderNumber;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
LeastExpensiveProduct SalesOrderID  
--------------------- ----------  
5.1865                SO43659  
419.4589              SO43660  
28.8404               SO43664
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de agregação &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [MAX &#40;Transact-SQL&#41;](../../t-sql/functions/max-transact-sql.md)   
 [Cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)  
  
  

