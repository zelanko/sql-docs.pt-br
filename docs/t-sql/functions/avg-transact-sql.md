---
title: AVG (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AVG_TSQL
- AVG
dev_langs:
- TSQL
helpviewer_keywords:
- AVG function [Transact-SQL]
- GROUP BY clause, AVG function
- DISTINCT keyword
- values [SQL Server], average
- average values
ms.assetid: 4534b705-d946-441b-9b5d-5fbe561c9131
caps.latest.revision: 52
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 80c1228faeaaa4012afc0fd27992a2f5cf389f6e
ms.openlocfilehash: 1e7598f8ee20f88346dfcbba1757f1173b34fe5c
ms.contentlocale: pt-br
ms.lasthandoff: 10/12/2017

---
# <a name="avg-transact-sql"></a>AVG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retorna a média dos valores em um grupo. Valores nulos são ignorados.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
AVG ( [ ALL | DISTINCT ] expression )  
   OVER ( [ partition_by_clause ] order_by_clause )    
```  
  
## <a name="arguments"></a>Argumentos  
ALL  
Aplica a função de agregação a todos os valores. ALL é o padrão.
  
DISTINCT  
Especifica que AVG será executado apenas uma vez em cada instância exclusiva de um valor, por mais que esse valor ocorra.
  
*expressão*  
É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de exato dados numéricos aproximados ou categoria de tipo, exceto para o **bit** tipo de dados. Funções de agregação e subconsultas não são permitidas.
  
SOBRE **(** [ *partition_by_clause* ] *order_by_clause***)**  
*partition_by_clause* divide o conjunto de resultados produzido pela cláusula FROM em partições para o qual a função é aplicada. Se não for especificado, a função tratará todas as linhas do conjunto de resultados da consulta como um único grupo. *order_by_clause* determina a ordem lógica na qual a operação é executada. *order_by_clause* é necessário. Para obter mais informações, consulte [a cláusula OVER &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).
  
## <a name="return-types"></a>Tipos de retorno
O tipo de retorno é determinado pelo tipo de resultado avaliado da *expressão*.
  
|Resultado da expressão|Tipo de retorno|  
|---|---|
|**tinyint**|**int**|  
|**smallint**|**int**|  
|**int**|**int**|  
|**bigint**|**bigint**|  
|**decimal** categoria (p, s)|**decimal (38, s)** dividido por **decimal (10, 0)**|  
|**Money** e **smallmoney** categoria|**money**|  
|**float** e **real** categoria|**float**|  
  
## <a name="remarks"></a>Comentários  
Se o tipo de dados *expressão* é um alias de dados tipo, o tipo de retorno também é do tipo de dados de alias. No entanto, se o tipo de dados básicos do tipo de dados de alias for promovido, por exemplo, de **tinyint** para **int**, é o valor de retorno dos dados promovidos tipo e não o tipo de dados de alias.
  
AVG () computa a média de um conjunto de valores, dividindo a soma desses valores pela contagem de valores não nulos. Se a soma exceder o valor máximo para o tipo de dados de valor de retorno, será retornado um erro.
  
AVG é uma função determinística quando usada sem as cláusulas OVER e ORDER BY. É não determinística quando especificada com as cláusulas OVER e ORDER BY. Para obter mais informações, veja [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-the-sum-and-avg-functions-for-calculations"></a>A. Usando as funções SUM e AVG para cálculos  
O exemplo a seguir calcula a média de horas de férias e a soma das horas de licença médica que os vice-presidentes da [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] usaram. Cada uma dessas funções de agregação produz um único valor de resumido para todas as linhas recuperadas. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].
  
```sql
SELECT AVG(VacationHours)AS 'Average vacation hours',   
    SUM(SickLeaveHours) AS 'Total sick leave hours'  
FROM HumanResources.Employee  
WHERE JobTitle LIKE 'Vice President%';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Average vacation hours       Total sick leave hours
 ----------------------       ----------------------
25                           97
  
(1 row(s) affected)
```
  
### <a name="b-using-the-sum-and-avg-functions-with-a-group-by-clause"></a>B. Usando as funções SUM e AVG com uma cláusula GROUP BY  
Quando usada com uma cláusula `GROUP BY`, cada função de agregação produz um único valor para cada grupo, em vez da tabela inteira. O exemplo a seguir produz valores resumidos para cada território de vendas no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. O resumo lista a média de bônus recebida pelo pessoal de vendas em cada território e a soma das vendas acumuladas no ano para cada território.
  
```sql
SELECT TerritoryID, AVG(Bonus)as 'Average bonus', SUM(SalesYTD) as 'YTD sales'  
FROM Sales.SalesPerson  
GROUP BY TerritoryID;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
TerritoryID Average Bonus         YTD Sales  
----------- --------------------- ---------------------  
NULL        0.00                  1252127.9471  
1           4133.3333             4502152.2674  
2           4100.00               3763178.1787  
3           2500.00               3189418.3662  
4           2775.00               6709904.1666  
5           6700.00               2315185.611  
6           2750.00               4058260.1825  
7           985.00                3121616.3202  
8           75.00                 1827066.7118  
9           5650.00               1421810.9242  
10          5150.00               4116871.2277  
  
(11 row(s) affected)  
```  
  
### <a name="c-using-avg-with-distinct"></a>C. Usando AVG com DISTINCT  
A instrução a seguir retorna o preço de tabela médio dos produtos no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Com a especificação de DISTINCT, somente valores exclusivos são considerados no cálculo.
  
```sql
SELECT AVG(DISTINCT ListPrice)  
FROM Production.Product;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
------------------------------
437.4042
  
(1 row(s) affected)
```
  
### <a name="d-using-avg-without-distinct"></a>D. Usando AVG sem DISTINCT  
Sem DISTINCT, a função `AVG` encontra o preço de tabela médio de todos os produtos na tabela `Product` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)], incluindo valores duplicados.
  
```sql
SELECT AVG(ListPrice)  
FROM Production.Product;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
------------------------------
438.6662
  
(1 row(s) affected)
```
  
### <a name="e-using-the-over-clause"></a>E. Usando a cláusula OVER  
O exemplo a seguir usa a função AVG com a cláusula OVER para fornecer uma média móvel de vendas anuais para cada território na tabela `Sales.SalesPerson` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Os dados são particionados por `TerritoryID` e ordenados logicamente por `SalesYTD`. Isso significa que a função AVG é computada para cada território com base no ano de vendas. Observe que para `TerritoryID` 1, há duas linhas para o ano de vendas 2005 que representam os dois vendedores com vendas nesse ano. As vendas médias para essas duas linhas são computadas e a terceira linha que representa vendas do ano 2006 é incluída na computação.
  
```sql
SELECT BusinessEntityID, TerritoryID   
   ,DATEPART(yy,ModifiedDate) AS SalesYear  
   ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
   ,CONVERT(varchar(20),AVG(SalesYTD) OVER (PARTITION BY TerritoryID   
                                            ORDER BY DATEPART(yy,ModifiedDate)   
                                           ),1) AS MovingAvg  
   ,CONVERT(varchar(20),SUM(SalesYTD) OVER (PARTITION BY TerritoryID   
                                            ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5  
ORDER BY TerritoryID,SalesYear;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
BusinessEntityID TerritoryID SalesYear   SalesYTD             MovingAvg            CumulativeTotal  
---------------- ----------- ----------- -------------------- -------------------- --------------------  
274              NULL        2005        559,697.56           559,697.56           559,697.56  
287              NULL        2006        519,905.93           539,801.75           1,079,603.50  
285              NULL        2007        172,524.45           417,375.98           1,252,127.95  
283              1           2005        1,573,012.94         1,462,795.04         2,925,590.07  
280              1           2005        1,352,577.13         1,462,795.04         2,925,590.07  
284              1           2006        1,576,562.20         1,500,717.42         4,502,152.27  
275              2           2005        3,763,178.18         3,763,178.18         3,763,178.18  
277              3           2005        3,189,418.37         3,189,418.37         3,189,418.37  
276              4           2005        4,251,368.55         3,354,952.08         6,709,904.17  
281              4           2005        2,458,535.62         3,354,952.08         6,709,904.17  
  
(10 row(s) affected)  
  
```  
  
Neste exemplo, a cláusula OVER não inclui PARTITION BY. Isso significa que a função será aplicada a todas as linhas retornadas pela consulta. A cláusula ORDER BY especificada na cláusula OVER determina a ordem lógica na qual a função AVG é aplicada. A consulta retorna uma média móvel de vendas por ano para todos os territórios de vendas especificados na cláusula WHERE. A cláusula ORDER BY especificada na instrução SELECT determina a ordem na qual as linhas da consulta são exibidas.
  
```sql
SELECT BusinessEntityID, TerritoryID   
   ,DATEPART(yy,ModifiedDate) AS SalesYear  
   ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
   ,CONVERT(varchar(20),AVG(SalesYTD) OVER (ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS MovingAvg  
   ,CONVERT(varchar(20),SUM(SalesYTD) OVER (ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5  
ORDER BY SalesYear;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
BusinessEntityID TerritoryID SalesYear   SalesYTD             MovingAvg            CumulativeTotal  
---------------- ----------- ----------- -------------------- -------------------- --------------------  
274              NULL        2005        559,697.56           2,449,684.05         17,147,788.35  
275              2           2005        3,763,178.18         2,449,684.05         17,147,788.35  
276              4           2005        4,251,368.55         2,449,684.05         17,147,788.35  
277              3           2005        3,189,418.37         2,449,684.05         17,147,788.35  
280              1           2005        1,352,577.13         2,449,684.05         17,147,788.35  
281              4           2005        2,458,535.62         2,449,684.05         17,147,788.35  
283              1           2005        1,573,012.94         2,449,684.05         17,147,788.35  
284              1           2006        1,576,562.20         2,138,250.72         19,244,256.47  
287              NULL        2006        519,905.93           2,138,250.72         19,244,256.47  
285              NULL        2007        172,524.45           1,941,678.09         19,416,780.93  
(10 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte também
[Funções de agregação &#40; Transact-SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[SOBRE cláusula &#40; Transact-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  

