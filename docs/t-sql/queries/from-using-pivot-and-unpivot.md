---
title: Usando PIVOT e UNPIVOT | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: PIVOT_TSQL
helpviewer_keywords:
- FROM clause, UNPIVOT operator
- unpivoting tables
- table pivoting [SQL Server]
- UNPIVOT operator
- crosstab query
- PIVOT operator
- rotating table-valued expressions
- pivoting tables
- FROM clause, PIVOT operator
- rotating columns
ms.assetid: 24ba54fc-98f7-4d35-8881-b5158aac1d66
caps.latest.revision: "35"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 4555a892c55ae8ef40e8fd0c3658412e3641d973
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="from---using-pivot-and-unpivot"></a>DE - usando PIVOT e UNPIVOT
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Você pode usar o `PIVOT` e `UNPIVOT` operadores relacionais para alterar uma expressão com valor de tabela em outra tabela. `PIVOT`gira uma expressão com valor de tabela ao transformar os valores exclusivos de uma coluna na expressão em várias colunas na saída e executa agregações onde forem necessárias em quaisquer valores de coluna remanescentes desejados na saída final. `UNPIVOT`executa a operação oposta a PIVOT, girando colunas de uma expressão com valor de tabela em valores de coluna.  
  
 A sintaxe para `PIVOT` fornece mais simples e mais legível do que a sintaxe que pode ser especificada em uma série complexa de contrário `SELECT...CASE` instruções. Para obter uma descrição completa da sintaxe para `PIVOT`, consulte [de (Transact-SQL)](../../t-sql/queries/from-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxe  
 A sintaxe a seguir resume como usar o `PIVOT` operador.  
  
```  
SELECT <non-pivoted column>,  
    [first pivoted column] AS <column name>,  
    [second pivoted column] AS <column name>,  
    ...  
    [last pivoted column] AS <column name>  
FROM  
    (<SELECT query that produces the data>)   
    AS <alias for the source query>  
PIVOT  
(  
    <aggregation function>(<column being aggregated>)  
FOR   
[<column that contains the values that will become column headers>]   
    IN ( [first pivoted column], [second pivoted column],  
    ... [last pivoted column])  
) AS <alias for the pivot table>  
<optional ORDER BY clause>;  
```  

## <a name="remarks"></a>Comentários  
Os identificadores de coluna no `UNPIVOT` cláusula siga o agrupamento de catálogo. Para [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], o agrupamento é sempre `SQL_Latin1_General_CP1_CI_AS`. Para [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] bancos de dados parcialmente independentes, o agrupamento é sempre `Latin1_General_100_CI_AS_KS_WS_SC`. Se a coluna for combinada com outras colunas e, em seguida, uma cláusula collate (`COLLATE DATABASE_DEFAULT`) é necessária para evitar conflitos.  

  
## <a name="basic-pivot-example"></a>Exemplo de PIVOT básico  
 O seguinte exemplo de código produz uma tabela de duas colunas que tem quatro linhas.  
  
```  
USE AdventureWorks2014 ;  
GO  
SELECT DaysToManufacture, AVG(StandardCost) AS AverageCost   
FROM Production.Product  
GROUP BY DaysToManufacture;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 DaysToManufacture AverageCost
 ----------------- -----------
 0                 5.0885
 1                 223.88
 2                 359.1082
 4                 949.4105
 ```
  
 Nenhum produto está definido com três `DaysToManufacture`.  
  
 O código a seguir exibe o mesmo resultado, dinamizado de forma que os valores `DaysToManufacture` tornem-se títulos de coluna. Uma coluna é criada para três dias `[3]`, embora os resultados sejam `NULL`.  
  
```  
-- Pivot table with one row and five columns  
SELECT 'AverageCost' AS Cost_Sorted_By_Production_Days,   
[0], [1], [2], [3], [4]  
FROM  
(SELECT DaysToManufacture, StandardCost   
    FROM Production.Product) AS SourceTable  
PIVOT  
(  
AVG(StandardCost)  
FOR DaysToManufacture IN ([0], [1], [2], [3], [4])  
) AS PivotTable;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
Cost_Sorted_By_Production_Days 0           1           2           3           4         
------------------------------ ----------- ----------- ----------- ----------- -----------
AverageCost                    5.0885      223.88      359.1082    NULL        949.4105
```
  
## <a name="complex-pivot-example"></a>Exemplo de PIVOT complexo  
 Um cenário comum em que `PIVOT` pode ser útil ocorre quando você deseja gerar relatórios de tabulação cruzada para resumir dados. Por exemplo, suponha que você deseje consultar a tabela `PurchaseOrderHeader` no banco de dados de exemplo `AdventureWorks2014` para determinar o número de ordens de compra colocadas por alguns funcionários. A consulta a seguir fornece esse relatório, ordenado por fornecedor.  
  
```  
USE AdventureWorks2014;  
GO  
SELECT VendorID, [250] AS Emp1, [251] AS Emp2, [256] AS Emp3, [257] AS Emp4, [260] AS Emp5  
FROM   
(SELECT PurchaseOrderID, EmployeeID, VendorID  
FROM Purchasing.PurchaseOrderHeader) p  
PIVOT  
(  
COUNT (PurchaseOrderID)  
FOR EmployeeID IN  
( [250], [251], [256], [257], [260] )  
) AS pvt  
ORDER BY pvt.VendorID;  
```  
  
 Este é um conjunto de resultados parcial.  
  
```
VendorID    Emp1        Emp2        Emp3        Emp4        Emp5  
----------- ----------- ----------- ----------- ----------- -----------
1492        2           5           4           4           4
1494        2           5           4           5           4
1496        2           4           4           5           5
1498        2           5           4           4           4
1500        3           4           4           5           4
```
  
 Os resultados retornados por essa instrução subselecionar são dinamizados na coluna `EmployeeID`.  
  
```  
SELECT PurchaseOrderID, EmployeeID, VendorID  
FROM PurchaseOrderHeader;  
```  
  
 Isso significa que os valores exclusivos retornados pela coluna `EmployeeID` tornam-se campos no conjunto de resultados final. Portanto, há uma coluna para cada número de `EmployeeID` especificado na cláusula pivot: neste caso, os funcionários `164`, `198`, `223`, `231` e `233`. A coluna `PurchaseOrderID` serve como a coluna de valor, contra a qual as colunas retornadas na saída final, que são chamadas de colunas de agrupamento, são agrupadas. Neste caso, as colunas de agrupamento são agregadas pela função `COUNT`. Observe que surge uma mensagem de aviso que indica que nenhum valor nulo que apareça na coluna `PurchaseOrderID` foi levado em conta ao computar a `COUNT` para cada funcionário.  
  
> [!IMPORTANT]  
>  Quando as funções de agregação são usadas com `PIVOT`, a presença de quaisquer valores nulos na coluna de valor não são considerados ao computar uma agregação.  
  
 `UNPIVOT`executa praticamente a operação inversa de `PIVOT`, girando colunas em linhas. Suponha que a tabela produzida no exemplo anterior seja armazenada no banco de dados como `pvt` e que você deseje girar os identificadores de coluna `Emp1`, `Emp2`, `Emp3`, `Emp4` e `Emp5` em valores de linhas que correspondam a um fornecedor específico. Isso significa que você deve identificar duas colunas adicionais. A coluna que conterá os valores de coluna que você está girando (`Emp1`, `Emp2`,...) será chamada `Employee`, e a coluna que conterá os valores que atualmente estão localizados nas colunas que estão sendo girados será chamada `Orders`. Essas colunas correspondem a *pivot_column* e *value_column*, respectivamente, no [!INCLUDE[tsql](../../includes/tsql-md.md)] definição. Aqui está a consulta.  
  
```  
-- Create the table and insert values as portrayed in the previous example.  
CREATE TABLE pvt (VendorID int, Emp1 int, Emp2 int,  
    Emp3 int, Emp4 int, Emp5 int);  
GO  
INSERT INTO pvt VALUES (1,4,3,5,4,4);  
INSERT INTO pvt VALUES (2,4,1,5,5,5);  
INSERT INTO pvt VALUES (3,4,3,5,4,4);  
INSERT INTO pvt VALUES (4,4,2,5,5,4);  
INSERT INTO pvt VALUES (5,5,1,5,5,5);  
GO  
-- Unpivot the table.  
SELECT VendorID, Employee, Orders  
FROM   
   (SELECT VendorID, Emp1, Emp2, Emp3, Emp4, Emp5  
   FROM pvt) p  
UNPIVOT  
   (Orders FOR Employee IN   
      (Emp1, Emp2, Emp3, Emp4, Emp5)  
)AS unpvt;  
GO  
```  
  
 Este é um conjunto de resultados parcial.  
  
```
VendorID    Employee    Orders
----------- ----------- ------
1            Emp1       4
1            Emp2       3 
1            Emp3       5
1            Emp4       4
1            Emp5       4
2            Emp1       4
2            Emp2       1
2            Emp3       5
2            Emp4       5
2            Emp5       5
...
```
  
 Observe que `UNPIVOT` não for o contrário exato de `PIVOT`. `PIVOT`executa uma agregação e, portanto, mescla possíveis linhas múltiplas em uma única linha na saída. `UNPIVOT`não reproduz o resultado da expressão de valor de tabela original porque as linhas foram mescladas. Além disso, null valores na entrada da `UNPIVOT` desaparecem na saída, enquanto que pode ter havido valores nulos originais na entrada antes do `PIVOT` operação.  
  
 O `Sales.vSalesPersonSalesByFiscalYears` exibir no [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] usa do banco de dados de exemplo `PIVOT` para retornar o total de vendas de cada vendedor em cada ano fiscal. Para o modo de exibição de script [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no **Pesquisador de objetos**, localize a exibição sob o **modos de exibição** pasta para o [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] banco de dados. O nome de exibição e, em seguida, selecione **exibição de Script como**.  
  
## <a name="see-also"></a>Consulte também  
 [DE (Transact-SQL)](../../t-sql/queries/from-transact-sql.md)   
 [CASO (Transact-SQL)](../../t-sql/language-elements/case-transact-sql.md)  
  
  
