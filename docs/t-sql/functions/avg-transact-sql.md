---
title: AVG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e97480b767e10a27c7e9647c2e6ae7369d4b37f8
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68040230"
---
# <a name="avg-transact-sql"></a>AVG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Essa função retorna a média dos valores em um grupo. Ela ignora valores nulos.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
AVG ( [ ALL | DISTINCT ] expression )  
   [ OVER ( [ partition_by_clause ] order_by_clause ) ]
```  
  
## <a name="arguments"></a>Argumentos  
ALL  
Aplica a função de agregação a todos os valores. ALL é o padrão.
  
DISTINTO  
Especifica que a AVG funciona apenas em uma instância exclusiva de cada valor, independentemente de quantas vezes o valor ocorre.
  
*expressão*  
Uma [expressão](../../t-sql/language-elements/expressions-transact-sql.md) da categoria de tipo de dados numéricos exatos ou aproximados, com exceção do tipo de dados **bit**. Funções de agregação e subconsultas não são permitidas.
  
OVER **(** [ *partition_by_clause* ] _order\_by\_clause_ **)**  
*partition_by_clause* divide o conjunto de resultados produzido pela cláusula FROM em partições às quais a função é aplicada. Se não for especificado, a função tratará todas as linhas do conjunto de resultados da consulta como um único grupo. A *order_by_clause* determina a ordem lógica na qual a operação é executada. *order_by_clause* é obrigatória. Para obter mais informações, consulte [Cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md).
  
## <a name="return-types"></a>Tipos de retorno
O resultado avaliado da *expressão* determina o tipo de retorno.
  
|Resultado da expressão|Tipo de retorno|  
|---|---|
|**tinyint**|**int**|  
|**smallint**|**int**|  
|**int**|**int**|  
|**bigint**|**bigint**|  
|Categoria **decimal** (p, s)|**decimal(38, min(s,6))**|  
|Categorias **money** e **smallmoney**|**money**|  
|Categorias **float** e **real**|**float**|  
  
## <a name="remarks"></a>Comentários  
Se o tipo de dados de *expression* for um tipo de dados de alias, o tipo de retorno também será do tipo de dados de alias. Entretanto, se o tipo de dados base do tipo de dados de alias for promovido, por exemplo, de **tinyint** para **int**, o valor retornado receberá o tipo de dados promovido, e não o tipo de dados de alias.
  
AVG () computa a média de um conjunto de valores, dividindo a soma desses valores pela contagem de valores não nulos. Se a soma exceder o valor máximo para o tipo de dados do valor retornado, a AVG() retornará um erro.
  
AVG é uma função determinística quando usada sem as cláusulas OVER e ORDER BY. É não determinística quando especificada com as cláusulas OVER e ORDER BY. Para obter mais informações, veja [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-the-sum-and-avg-functions-for-calculations"></a>a. Usando as funções SUM e AVG para cálculos  
Este exemplo calcula a média de horas de férias e a soma das horas de licença médica que os vice-presidentes da [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] usaram. Cada uma dessas funções de agregação produz um único valor de resumido para todas as linhas recuperadas. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].
  
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
Quando usada com uma cláusula `GROUP BY`, cada função de agregação produz um único valor que abrange cada grupo, em vez de um único valor para a tabela inteira. O exemplo a seguir produz valores resumidos para cada território de vendas do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. O resumo lista a média de bônus recebida pelo pessoal de vendas em cada território e a soma das vendas acumuladas no ano para cada território.
  
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
Essa instrução retorna o preço de tabela médio dos produtos no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Com o uso de DISTINCT, o cálculo considera apenas valores exclusivos.
  
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
O exemplo a seguir usa a função AVG com a cláusula OVER para fornecer uma média móvel de vendas anuais para cada território da tabela `Sales.SalesPerson` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Os dados são particionados por `TerritoryID` e ordenados logicamente por `SalesYTD`. Isso significa que a função AVG é computada para cada território com base no ano de vendas. Observe que para `TerritoryID` 1, há duas linhas para o ano de vendas 2005 que representam os dois vendedores com vendas nesse ano. As vendas médias dessas duas linhas são calculadas e, em seguida, a terceira linha que representa as vendas do ano 2006 é incluída no cálculo.
  
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
  
Neste exemplo, a cláusula OVER não inclui PARTITION BY. Isso significa que a função será aplicada a todas as linhas retornadas pela consulta. A cláusula ORDER BY especificada na cláusula OVER determina a ordem lógica na qual a função AVG é aplicada. A consulta retorna uma média móvel de vendas por ano para todos os territórios de vendas especificados na cláusula WHERE. A cláusula ORDER BY especificada na instrução SELECT determina a ordem na qual a instrução SELECT exibe as linhas da consulta.
  
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
  
## <a name="see-also"></a>Confira também
[Funções de agregação &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[Cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  
