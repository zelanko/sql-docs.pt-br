---
title: "CLASSIFICAÇÃO (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 10/25/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RANK
- RANK_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- row ranking [SQL Server]
- tied rows [SQL Server]
- ranking rows
- RANK function [Transact-SQL]
ms.assetid: 2d96f6d2-5db7-4b3c-a63e-213c58e4af55
caps.latest.revision: 62
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 304ceaedefe1755c56b27a8f6e64a922a1986bc0
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="rank-transact-sql"></a>RANK (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna a classificação de cada linha na partição de um conjunto de resultados. A classificação de uma linha é um mais o número de classificações que vêm antes da linha em questão.  

  ROW_NUMBER e classificação são semelhantes. Números ROW_NUMBER todas as linhas em sequência (por exemplo 1, 2, 3, 4, 5). CLASSIFICAÇÃO fornece o mesmo valor numérico para ties (por exemplo 1, 2, 2, 4, 5).   
  
> [!NOTE]
> A classificação é que um valor temporário calculados quando a consulta é executada. Para manter os números em uma tabela, consulte [propriedade IDENTITY](../../t-sql/statements/create-table-transact-sql-identity-property.md) e [SEQUÊNCIA](../../t-sql/statements/create-sequence-transact-sql.md). 
   
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
RANK ( ) OVER ( [ partition_by_clause ] order_by_clause )  
```  
  
## <a name="arguments"></a>Argumentos  
 SOBRE **(** [ *partition_by_clause* ] *order_by_clause***)**  
 *partition_by_clause* divide o conjunto de resultados produzido pela cláusula FROM em partições para o qual a função é aplicada. Se não for especificado, a função tratará todas as linhas do conjunto de resultados da consulta como um único grupo. *order_by_clause* determina a ordem dos dados antes da função é aplicada. O *order_by_clause* é necessário. O \<cláusula rows ou range > da OVER cláusula não pode ser especificada para a função de classificação. Para obter mais informações, consulte [a cláusula OVER &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Tipos de retorno  
 **bigint**  
  
## <a name="remarks"></a>Comentários  
 Se duas ou mais linhas empatarem em uma classificação, cada linha empatada receberá a mesma classificação. Por exemplo, se os dois melhores vendedores tiverem o mesmo valor SalesYTD, ambos serão classificados com o número um. O vendedor com o próximo SalesYTD maior será classificado com o número três, porque há duas linhas com classificação mais alta. Portanto, a função RANK nem sempre retorna inteiros consecutivos.  
  
 A ordem de classificação usada para a consulta inteira determina a ordem na qual as linhas aparecem em um conjunto de resultados.  
  
 RANK é não determinístico. Para obter mais informações, veja [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-ranking-rows-within-a-partition"></a>A. Classificando linhas dentro de uma partição  
 O exemplo a seguir classifica os produtos em inventário nos locais de inventário especificados de acordo com suas quantidades. O conjunto de resultados é particionado por `LocationID` e ordenado logicamente por `Quantity`. Observe que produtos 494 e 495 têm a mesma quantidade. Como eles estão vinculados, ambos são classificados como um.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT i.ProductID, p.Name, i.LocationID, i.Quantity  
    ,RANK() OVER   
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
  
ProductID   Name                   LocationID   Quantity Rank  
----------- ---------------------- ------------ -------- ----  
494         Paint - Silver         3            49       1  
495         Paint - Blue           3            49       1  
493         Paint - Red            3            41       3  
496         Paint - Yellow         3            30       4  
492         Paint - Black          3            17       5  
495         Paint - Blue           4            35       1  
496         Paint - Yellow         4            25       2  
493         Paint - Red            4            24       3  
492         Paint - Black          4            14       4  
494         Paint - Silver         4            12       5  
 (10 row(s) affected)  
```  
  
### <a name="b-ranking-all-rows-in-a-result-set"></a>B. Classificando todas as linhas em um conjunto de resultados  
 O exemplo a seguir retorna os dez primeiros funcionários classificados pelo salário. Como uma cláusula de PARTITION BY não foi especificada, a função RANK foi aplicada a todas as linhas no conjunto de resultados.  
  
```  
USE AdventureWorks2012  
SELECT TOP(10) BusinessEntityID, Rate,   
       RANK() OVER (ORDER BY Rate DESC) AS RankBySalary  
FROM HumanResources.EmployeePayHistory AS eph1  
WHERE RateChangeDate = (SELECT MAX(RateChangeDate)   
                        FROM HumanResources.EmployeePayHistory AS eph2  
                        WHERE eph1.BusinessEntityID = eph2.BusinessEntityID)  
ORDER BY BusinessEntityID;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID Rate                  RankBySalary  
---------------- --------------------- --------------------  
1                125.50                1  
2                63.4615               4  
3                43.2692               8  
4                29.8462               19  
5                32.6923               16  
6                32.6923               16  
7                50.4808               6  
8                40.8654               10  
9                40.8654               10  
10               42.4808               9  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-ranking-rows-within-a-partition"></a>C: classificando linhas dentro de uma partição  
 O exemplo a seguir classifica os representantes de vendas de acordo com o total de vendas de cada região de vendas. O conjunto de linhas é particionado por `SalesTerritoryGroup` e ordenado por `SalesAmountQuota`.  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUM(SalesAmountQuota) AS TotalSales, SalesTerritoryRegion,  
    RANK() OVER (PARTITION BY SalesTerritoryRegion ORDER BY SUM(SalesAmountQuota) DESC ) AS RankResult  
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq ON e.EmployeeKey = sq.EmployeeKey  
INNER JOIN dbo.DimSalesTerritory AS st ON e.SalesTerritoryKey = st.SalesTerritoryKey  
WHERE SalesPersonFlag = 1 AND SalesTerritoryRegion != N'NA'  
GROUP BY LastName, SalesTerritoryRegion;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
LastName          TotalSales     SalesTerritoryGroup  RankResult
----------------  -------------  -------------------  --------
Tsoflias          1687000.0000   Australia            1
Saraiva           7098000.0000   Canada               1
Vargas            4365000.0000   Canada               2
Carson            12198000.0000  Central              1
Varkey Chudukatil 5557000.0000   France               1
Valdez            2287000.0000   Germany              1
Blythe            11162000.0000  Northeast            1
Campbell          4025000.0000   Northwest            1
Ansman-Wolfe      3551000.0000   Northwest            2
Mensa-Annan       2753000.0000   Northwest            3
Reiter            8541000.0000   Southeast            1
Mitchell          11786000.0000  Southwest            1
Ito               7804000.0000   Southwest            2
Pak               10514000.0000  United Kingdom       1
```  
  
## <a name="see-also"></a>Consulte também  
 [DENSE_RANK &#40; Transact-SQL &#41;](../../t-sql/functions/dense-rank-transact-sql.md)   
 [ROW_NUMBER &#40; Transact-SQL &#41;](../../t-sql/functions/row-number-transact-sql.md)   
 [NTILE &#40; Transact-SQL &#41;](../../t-sql/functions/ntile-transact-sql.md)   
 [Classificação de funções &#40; Transact-SQL &#41;](../../t-sql/functions/ranking-functions-transact-sql.md)   
 [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  




