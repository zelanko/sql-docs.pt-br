---
title: ROW_NUMBER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ROW_NUMBER
- ROW_NUMBER_TSQL
- ROW_NUMBER()_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ROW_NUMBER function
- row numbers [SQL Server]
- sequential row numbers [SQL Server]
ms.assetid: 82fa9016-77db-4b42-b4c8-df6095b81906
caps.latest.revision: 50
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 820acddf7de1282501caf2fcaa43dbc757b98b7a
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="rownumber-transact-sql"></a>ROW_NUMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Definem a saída de um resultado de números. Mais especificamente, retorna o número sequencial de uma linha dentro de uma partição de um conjunto de resultados, começando em 1 para a primeira linha em cada partição. 
  
`ROW_NUMBER`e `RANK` são semelhantes. `ROW_NUMBER`números de todas as linhas em sequência (por exemplo 1, 2, 3, 4, 5). `RANK`fornece o mesmo valor numérico para ties (por exemplo 1, 2, 2, 4, 5).   
  
> [!NOTE]
> `ROW_NUMBER`é um valor temporário calculado quando a consulta é executada. Para manter os números em uma tabela, consulte [propriedade IDENTITY](../../t-sql/statements/create-table-transact-sql-identity-property.md) e [SEQUÊNCIA](../../t-sql/statements/create-sequence-transact-sql.md). 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
 
  
## <a name="syntax"></a>Sintaxe  
  
```  
ROW_NUMBER ( )   
    OVER ( [ PARTITION BY value_expression , ... [ n ] ] order_by_clause )  
```  
  
## <a name="arguments"></a>Argumentos  
 PARTITION BY *value_expression*  
 Divide o conjunto de resultados produzido pelo [FROM](../../t-sql/queries/from-transact-sql.md) cláusula em partições às quais a função ROW_NUMBER é aplicada. *value_expression* Especifica a coluna pela qual o conjunto de resultados é particionado. Se `PARTITION BY` não for especificado, a função tratará todas as linhas do conjunto como um único grupo de resultados de consulta. Para obter mais informações, consulte [a cláusula OVER &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
 *order_by_clause*  
 O `ORDER BY` cláusula determina a sequência na qual as linhas são atribuídas seus exclusivo `ROW_NUMBER` dentro de uma partição especificada. É obrigatório. Para obter mais informações, consulte [a cláusula OVER &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Tipos de retorno  
 **bigint**  
  
## <a name="general-remarks"></a>Comentários gerais  
 Não há nenhuma garantia de que as linhas retornadas por uma consulta usando `ROW_NUMBER()` serão ordenadas exatamente os mesmos, com cada execução, a menos que as seguintes condições forem verdadeiras.  
  
1.  Os valores da coluna particionada sejam exclusivos.  
  
2.  Valores da `ORDER BY` colunas são exclusivas.  
  
3.  Combinações de valores da coluna de partição e `ORDER BY` colunas são exclusivas.  
  
 `ROW_NUMBER()`é não determinística. Para obter mais informações, veja [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-simple-examples"></a>A. Exemplos simples 

A consulta a seguir retorna as tabelas do quatro sistema em ordem alfabética.

```
SELECT 
  name, recovery_model_desc
FROM sys.databases 
WHERE database_id < 5
ORDER BY name ASC;
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|name    |recovery_model_desc |  
|-----------  |------------ |  
|mestre |SIMPLE |
|modelo |FULL |
|msdb |SIMPLE |
|tempdb |SIMPLE |

Para adicionar uma coluna de número de linha na frente de cada linha, adicionar uma coluna com o `ROW_NUMBER` função, nesse caso denominada `Row#`. Você deve mover o `ORDER BY` cláusula até o `OVER` cláusula.

```
SELECT 
  ROW_NUMBER() OVER(ORDER BY name ASC) AS Row#,
  name, recovery_model_desc
FROM sys.databases 
WHERE database_id < 5;
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|N º de linha |name    |recovery_model_desc |  
|------- |-----------  |------------ |  
|1 |mestre |SIMPLE |
|2 |modelo |FULL |
|3 |msdb |SIMPLE |
|4 |tempdb |SIMPLE |

Adicionando um `PARTITION BY` cláusula o `recovery_model_desc` coluna reiniciará a numeração quando o `recovery_model_desc` o valor é alterado. 
 
```
SELECT 
  ROW_NUMBER() OVER(PARTITION BY recovery_model_desc ORDER BY name ASC) 
    AS Row#,
  name, recovery_model_desc
FROM sys.databases WHERE database_id < 5;
```  

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|N º de linha |name    |recovery_model_desc |  
|------- |-----------  |------------ |  
|1 |modelo |FULL |
|1 |mestre |SIMPLE |
|2 |msdb |SIMPLE |
|3 |tempdb |SIMPLE |


### <a name="b-returning-the-row-number-for-salespeople"></a>B. Retornando o número de linha para vendedores  
 O exemplo a seguir calcula um número de linha para os vendedores da [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] com base em sua classificação de vendas no ano até a data.  
  
```  
USE AdventureWorks2012;   
GO  
SELECT ROW_NUMBER() OVER(ORDER BY SalesYTD DESC) AS Row,   
    FirstName, LastName, ROUND(SalesYTD,2,1) AS "Sales YTD"   
FROM Sales.vSalesPerson  
WHERE TerritoryName IS NOT NULL AND SalesYTD <> 0;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
Row FirstName    LastName               SalesYTD  
--- -----------  ---------------------- -----------------  
1   Linda        Mitchell               4251368.54  
2   Jae          Pak                    4116871.22  
3   Michael      Blythe                 3763178.17  
4   Jillian      Carson                 3189418.36  
5   Ranjit       Varkey Chudukatil      3121616.32  
6   José         Saraiva                2604540.71  
7   Shu          Ito                    2458535.61  
8   Tsvi         Reiter                 2315185.61  
9   Rachel       Valdez                 1827066.71  
10  Tete         Mensa-Annan            1576562.19  
11  David        Campbell               1573012.93  
12  Garrett      Vargas                 1453719.46  
13  Lynn         Tsoflias               1421810.92  
14  Pamela       Ansman-Wolfe           1352577.13  
```  
  
### <a name="c-returning-a-subset-of-rows"></a>C. Retornando um subconjunto de linhas  
 O exemplo a seguir calcula números de linha para todas as linhas da tabela `SalesOrderHeader` na ordem de `OrderDate` e retorna somente as linhas de `50` a `60`.  
  
```  
USE AdventureWorks2012;  
GO  
WITH OrderedOrders AS  
(  
    SELECT SalesOrderID, OrderDate,  
    ROW_NUMBER() OVER (ORDER BY OrderDate) AS RowNumber  
    FROM Sales.SalesOrderHeader   
)   
SELECT SalesOrderID, OrderDate, RowNumber    
FROM OrderedOrders   
WHERE RowNumber BETWEEN 50 AND 60;  
```  
  
### <a name="d-using-rownumber-with-partition"></a>D. Usando ROW_NUMBER () com PARTITION  
 O exemplo a seguir usa o argumento `PARTITION BY` para particionar o conjunto de resultados da consulta pela coluna `TerritoryName`. A cláusula `ORDER BY` especificada na cláusula `OVER` ordena as linhas em cada partição pela coluna `SalesYTD`. A cláusula `ORDER BY` na instrução `SELECT` ordena o conjunto de resultados inteiro da consulta por `TerritoryName`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT FirstName, LastName, TerritoryName, ROUND(SalesYTD,2,1) AS SalesYTD,  
ROW_NUMBER() OVER(PARTITION BY TerritoryName ORDER BY SalesYTD DESC) 
  AS Row  
FROM Sales.vSalesPerson  
WHERE TerritoryName IS NOT NULL AND SalesYTD <> 0  
ORDER BY TerritoryName;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
FirstName  LastName             TerritoryName        SalesYTD      Row  
---------  -------------------- ------------------   ------------  ---  
Lynn       Tsoflias             Australia            1421810.92    1  
José       Saraiva              Canada               2604540.71    1  
Garrett    Vargas               Canada               1453719.46    2  
Jillian    Carson               Central              3189418.36    1  
Ranjit     Varkey Chudukatil    France               3121616.32    1  
Rachel     Valdez               Germany              1827066.71    1  
Michael    Blythe               Northeast            3763178.17    1  
Tete       Mensa-Annan          Northwest            1576562.19    1  
David      Campbell             Northwest            1573012.93    2  
Pamela     Ansman-Wolfe         Northwest            1352577.13    3  
Tsvi       Reiter               Southeast            2315185.61    1  
Linda      Mitchell             Southwest            4251368.54    1  
Shu        Ito                  Southwest            2458535.61    2  
Jae        Pak                  United Kingdom       4116871.22    1  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-returning-the-row-number-for-salespeople"></a>E. Retornando o número de linha para vendedores  
 O exemplo a seguir retorna o `ROW_NUMBER` para representantes de vendas com base em suas cotas de vendas atribuída.  
  
```  
-- Uses AdventureWorks  
  
SELECT ROW_NUMBER() OVER(ORDER BY SUM(SalesAmountQuota) DESC) 
    AS RowNumber,  
    FirstName, LastName,   
    CONVERT(varchar(13), SUM(SalesAmountQuota),1) AS SalesQuota   
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq  
    ON e.EmployeeKey = sq.EmployeeKey  
WHERE e.SalesPersonFlag = 1  
GROUP BY LastName, FirstName;  
```  
  
 Este é um conjunto de resultados parcial.  
  
 ```
RowNumber  FirstName  LastName            SalesQuota
---------  ---------  ------------------  -------------
1          Jillian    Carson              12,198,000.00
2          Linda      Mitchell            11,786,000.00
3          Michael    Blythe              11,162,000.00
4          Jae        Pak                 10,514,000.00
 ```  
  
### <a name="f-using-rownumber-with-partition"></a>F. Usando ROW_NUMBER () com PARTITION  
 O exemplo a seguir mostra o uso da função `ROW_NUMBER` com o argumento `PARTITION BY`. Isso faz com que o `ROW_NUMBER` função para numerar linhas em cada partição.  
  
```  
-- Uses AdventureWorks  
  
SELECT ROW_NUMBER() OVER(PARTITION BY SalesTerritoryKey 
        ORDER BY SUM(SalesAmountQuota) DESC) AS RowNumber,  
    LastName, SalesTerritoryKey AS Territory,  
    CONVERT(varchar(13), SUM(SalesAmountQuota),1) AS SalesQuota   
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq  
    ON e.EmployeeKey = sq.EmployeeKey  
WHERE e.SalesPersonFlag = 1  
GROUP BY LastName, FirstName, SalesTerritoryKey;  
```  
  
 Este é um conjunto de resultados parcial.  
  
 ```
RowNumber  LastName            Territory  SalesQuota
---------  ------------------  ---------  -------------
1          Campbell            1           4,025,000.00
2          Ansman-Wolfe        1           3,551,000.00
3          Mensa-Annan         1           2,275,000.00
1          Blythe              2          11,162,000.00
1          Carson              3          12,198,000.00
1          Mitchell            4          11,786,000.00
2          Ito                 4           7,804,000.00
 ```  
  
## <a name="see-also"></a>Consulte também  
 [Classificação &#40; Transact-SQL &#41;](../../t-sql/functions/rank-transact-sql.md)   
 [DENSE_RANK &#40; Transact-SQL &#41;](../../t-sql/functions/dense-rank-transact-sql.md)   
 [NTILE &#40; Transact-SQL &#41;](../../t-sql/functions/ntile-transact-sql.md)  
  
  



