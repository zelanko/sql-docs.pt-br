---
title: DENSE_RANK (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DENSE_RANK_TSQL
- DENSE_RANK
dev_langs:
- TSQL
helpviewer_keywords:
- row ranking [SQL Server]
- DENSE_RANK function
- tied rows [SQL Server]
- ranking rows
ms.assetid: 03871fc6-9592-4016-b0b2-ff543f132b20
caps.latest.revision: 47
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4897ba682387179ad305657215afce9cde3e5a70
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="denserank-transact-sql"></a>DENSE_RANK (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna a classificação de linhas dentro da partição de um conjunto de resultados, sem qualquer lacuna na classificação. A classificação de uma linha é um mais o número de classificações distintas que vêm antes da linha em questão.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DENSE_RANK ( ) OVER ( [ <partition_by_clause> ] < order_by_clause > )  
```  
  
## <a name="arguments"></a>Argumentos  
 \<partition_by_clause >  
 Divide o conjunto de resultados produzido pelo [FROM](../../t-sql/queries/from-transact-sql.md) cláusula em partições às quais a função DENSE_RANK é aplicada. Para obter a sintaxe PARTITION BY, consulte [a cláusula OVER &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
 \<order_by_clause >  
 Determina a ordem na qual a função DENSE_RANK é aplicada às linhas em uma partição.  
  
## <a name="return-types"></a>Tipos de retorno  
 **bigint**  
  
## <a name="remarks"></a>Comentários  
 Se duas ou mais linhas empatarem em uma classificação na mesma partição, cada linha empatada receberá a mesma classificação. Por exemplo, se os dois melhores vendedores tiverem o mesmo valor SalesYTD, ambos serão classificados com o número um. O vendedor com o próximo SalesYTD mais alto será classificado com o número dois. Esse será um número maior que o número de linhas distintas que vêm antes dessa linha. Portanto, os números retornados pela função DENSE_RANK não têm lacunas e sempre têm classificações consecutivas.  
  
 A ordem de classificação usada para a consulta inteira determina a ordem na qual as linhas são exibidas em um resultado. Isso significa que uma linha classificada com o número um não precisa ser a primeira linha da partição.  
  
 DENSE_RANK é não determinística. Para obter mais informações, veja [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-ranking-rows-within-a-partition"></a>A. Classificando linhas dentro de uma partição  
 O exemplo a seguir classifica os produtos em inventário nos locais de inventário especificados de acordo com suas quantidades. O conjunto de resultados é particionado por `LocationID` e ordenado logicamente por `Quantity`. Observe que produtos 494 e 495 têm a mesma quantidade. Como eles estão vinculados, ambos são classificados como um.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT i.ProductID, p.Name, i.LocationID, i.Quantity  
    ,DENSE_RANK() OVER   
    (PARTITION BY i.LocationID ORDER BY i.Quantity DESC) AS Rank  
FROM Production.ProductInventory AS i   
INNER JOIN Production.Product AS p   
    ON i.ProductID = p.ProductID  
WHERE i.LocationID BETWEEN 3 AND 4  
ORDER BY i.LocationID;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
ProductID   Name                               LocationID Quantity Rank  
----------- ---------------------------------- ---------- -------- -----  
494         Paint - Silver                     3          49       1  
495         Paint - Blue                       3          49       1  
493         Paint - Red                        3          41       2  
496         Paint - Yellow                     3          30       3  
492         Paint - Black                      3          17       4  
495         Paint - Blue                       4          35       1  
496         Paint - Yellow                     4          25       2  
493         Paint - Red                        4          24       3  
492         Paint - Black                      4          14       4  
494         Paint - Silver                     4          12       5  
  
(10 row(s) affected)  
  
```  
  
### <a name="b-ranking-all-rows-in-a-result-set"></a>B. Classificando todas as linhas em um conjunto de resultados  
 O exemplo a seguir retorna os dez primeiros funcionários classificados pelo salário. Como uma cláusula PARTITION BY não foi especificada, a função DENSE_RANK foi aplicada a todas as linhas no conjunto de resultados.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT TOP(10) BusinessEntityID, Rate,   
       DENSE_RANK() OVER (ORDER BY Rate DESC) AS RankBySalary  
FROM HumanResources.EmployeePayHistory;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID Rate                  RankBySalary  
---------------- --------------------- --------------------  
1                125.50                1  
25               84.1346               2  
273              72.1154               3  
2                63.4615               4  
234              60.0962               5  
263              50.4808               6  
7                50.4808               6  
234              48.5577               7  
285              48.101                8  
274              48.101                8  
```  
  
## <a name="c-four-ranking-functions-used-in-the-same-query"></a>C. Quatro funções de classificação usadas na mesma consulta  
 A seguir, mostramos as quatro funções de classificação usadas na mesma consulta. Para obter exemplos específicos de função, consulte cada função de classificação.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName  
    ,ROW_NUMBER() OVER (ORDER BY a.PostalCode) AS "Row Number"  
    ,RANK() OVER (ORDER BY a.PostalCode) AS Rank  
    ,DENSE_RANK() OVER (ORDER BY a.PostalCode) AS "Dense Rank"  
    ,NTILE(4) OVER (ORDER BY a.PostalCode) AS Quartile  
    ,s.SalesYTD  
    ,a.PostalCode  
FROM Sales.SalesPerson AS s   
    INNER JOIN Person.Person AS p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address AS a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL AND SalesYTD <> 0;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|FirstName|LastName|Row Number|Rank|Dense Rank|Quartile|SalesYTD|PostalCode|  
|---------------|--------------|----------------|----------|----------------|--------------|--------------|----------------|  
|Michael|Blythe|1|1|1|1|4557045.0459|98027|  
|Linda|Mitchell|2|1|1|1|5200475.2313|98027|  
|Jillian|Carson|3|1|1|1|3857163.6332|98027|  
|Garrett|Vargas|4|1|1|1|1764938.9859|98027|  
|Tsvi|Reiter|5|1|1|2|2811012.7151|98027|  
|Shu|Ito|6|6|2|2|3018725.4858|98055|  
|José|Saraiva|7|6|2|2|3189356.2465|98055|  
|David|Campbell|8|6|2|3|3587378.4257|98055|  
|Tete|Mensa-Annan|9|6|2|3|1931620.1835|98055|  
|Lynn|Tsoflias|10|6|2|3|1758385.926|98055|  
|Rachel|Valdez|11|6|2|4|2241204.0424|98055|  
|Jae|Pak|12|6|2|4|5015682.3752|98055|  
|Ranjit|Varkey Chudukatil|13|6|2|4|3827950.238|98055| 


## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-ranking-rows-within-a-partition"></a>D: classificando linhas dentro de uma partição  
 O exemplo a seguir classifica os representantes de vendas de acordo com o total de vendas de cada região de vendas. O conjunto de linhas é particionado por `SalesTerritoryGroup` e ordenado por `SalesAmountQuota`.  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUM(SalesAmountQuota) AS TotalSales, SalesTerritoryGroup,  
    DENSE_RANK() OVER (PARTITION BY SalesTerritoryGroup ORDER BY SUM(SalesAmountQuota) DESC ) AS RankResult  
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq ON e.EmployeeKey = sq.EmployeeKey  
INNER JOIN dbo.DimSalesTerritory AS st ON e.SalesTerritoryKey = st.SalesTerritoryKey  
WHERE SalesPersonFlag = 1 AND SalesTerritoryGroup != N'NA'  
GROUP BY LastName,SalesTerritoryGroup;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `LastName          TotalSales     SalesTerritoryGroup  RankResult`  
  
 `----------------  -------------  -------------------  --------`  
  
 `Pak               10514000.0000  Europe               1`  
  
 `Varkey Chudukatil  5557000.0000  Europe               2`  
  
 `Valdez             2287000.0000  Europe               3`  
  
 `Carson            12198000.0000  North America        1`  
  
 `Mitchell          11786000.0000  North America        2`  
  
 `Blythe            11162000.0000  North America        3`  
  
 `Reiter             8541000.0000  North America        4`  
  
 `Ito                7804000.0000  North America        5`  
  
 `Saraiva            7098000.0000  North America        6`  
  
 `Vargas             4365000.0000  North America        7`  
  
 `Campbell           4025000.0000  North America        8`  
  
 `Ansman-Wolfe       3551000.0000  North America        9`  
  
 `Mensa-Annan        2753000.0000  North America        10`  
  
 `Tsoflias           1687000.0000  Pacific              1`  
  



## <a name="see-also"></a>Consulte também  
 [Classificação &#40; Transact-SQL &#41;](../../t-sql/functions/rank-transact-sql.md)   
 [ROW_NUMBER &#40; Transact-SQL &#41;](../../t-sql/functions/row-number-transact-sql.md)   
 [NTILE &#40; Transact-SQL &#41;](../../t-sql/functions/ntile-transact-sql.md)   
 [Classificação de funções &#40; Transact-SQL &#41;](../../t-sql/functions/ranking-functions-transact-sql.md)   
 [Funções](../../t-sql/functions/functions.md)  
  
  


