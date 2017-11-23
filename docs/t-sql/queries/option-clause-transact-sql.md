---
title: "Cláusula OPTION (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPTION clause
- OPTION_TSQL
- OPTION
- OPTION_clause_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- clauses [SQL Server], OPTION
- OPTION clause
ms.assetid: f47e2f3f-9302-4711-9d66-16b1a2a7ffe3
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b5457a572985c9a83984efbe9ce90811e22cf2d4
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="option-clause-transact-sql"></a>Cláusula OPTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Especifica que a dica de consulta indicada deve ser usada em toda a consulta. Cada dica de consulta pode ser especificada apenas uma vez, embora sejam permitidas várias dicas de consulta. Somente uma cláusula OPTION pode ser especificada com a instrução.  
  
 Esta cláusula pode ser especificada nas instruções SELECT, DELETE, UPDATE e MERGE.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
[ OPTION ( <query_hint> [ ,...n ] ) ]   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
OPTION ( <query_option> [ ,...n ] )  
  
<query_option> ::=  
    LABEL = label_name |  
    <query_hint>  
  
<query_hint> ::=  
    HASH JOIN   
    | LOOP JOIN   
    | MERGE JOIN  
    | FORCE ORDER  
    | { FORCE | DISABLE } EXTERNALPUSHDOWN  
```  
  
## <a name="arguments"></a>Argumentos  
 *query_hint*  
 Palavras-chave que indicam as dicas de otimização são usadas para personalizar a forma como o Mecanismo de Banco de Dados processa a instrução. Para obter mais informações, veja [Dicas de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-an-option-clause-with-a-group-by-clause"></a>A. Usando uma cláusula OPTION com uma cláusula GROUP BY  
 O exemplo a seguir mostra como a cláusula `OPTION` é usada com uma cláusula `GROUP BY`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, OrderQty, SUM(LineTotal) AS Total  
FROM Sales.SalesOrderDetail  
WHERE UnitPrice < $5.00  
GROUP BY ProductID, OrderQty  
ORDER BY ProductID, OrderQty  
OPTION (HASH GROUP, FAST 10);  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-select-statement-with-a-label-in-the-option-clause"></a>B. Instrução SELECT com um rótulo na cláusula OPTION  
 O exemplo a seguir mostra um simples [!INCLUDE[ssDW](../../includes/ssdw-md.md)] instrução SELECT com um rótulo na cláusula OPTION.  
  
```  
-- Uses AdventureWorks  
  
SELECT * FROM FactResellerSales  
  OPTION ( LABEL = 'q17' );  
```  
  
### <a name="c-select-statement-with-a-query-hint-in-the-option-clause"></a>C. Instrução SELECT com uma dica de consulta na cláusula OPTION  
 O exemplo a seguir mostra uma instrução SELECT que usa uma dica de consulta HASH JOIN na cláusula OPTION.  
  
```  
-- Uses AdventureWorks  
  
SELECT COUNT (*) FROM dbo.DimCustomer a  
INNER JOIN dbo.FactInternetSales b   
ON (a.CustomerKey = b.CustomerKey)  
OPTION (HASH JOIN);  
```  
  
### <a name="d-select-statement-with-a-label-and-multiple-query-hints-in-the-option-clause"></a>D. Instrução SELECT com um rótulo e várias dicas de consulta na cláusula OPTION  
 O exemplo a seguir é um [!INCLUDE[ssDW](../../includes/ssdw-md.md)] instrução SELECT que contém um rótulo e várias dicas de consulta. Quando a consulta é executada em nós de computação, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplicará uma junção de hash ou junção de mesclagem, de acordo com a estratégia que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] decide é o ideal.  
  
```  
-- Uses AdventureWorks  
  
SELECT COUNT (*) FROM dbo.DimCustomer a  
INNER JOIN dbo.FactInternetSales b   
ON (a.CustomerKey = b.CustomerKey)  
OPTION ( Label = 'CustJoin', HASH JOIN, MERGE JOIN);  
```  
  
### <a name="e-using-a-query-hint-when-querying-a-view"></a>E. Usando uma dica de consulta ao consultar uma exibição  
 O exemplo a seguir cria uma exibição chamada CustomerView e, em seguida, usa uma dica de consulta HASH JOIN em uma consulta que faz referência a um modo de exibição e uma tabela.  
  
```  
-- Uses AdventureWorks  
  
CREATE VIEW CustomerView  
AS  
SELECT CustomerKey, FirstName, LastName FROM ssawPDW..DimCustomer;  
  
SELECT COUNT (*) FROM dbo.CustomerView a  
INNER JOIN dbo.FactInternetSales b  
ON (a.CustomerKey = b.CustomerKey)  
OPTION (HASH JOIN);  
  
DROP VIEW CustomerView;  
  
```  
  
### <a name="f-query-with-a-subselect-and-a-query-hint"></a>F. Consulta com uma Subseleção e uma dica de consulta  
 O exemplo a seguir mostra uma consulta que contenha uma Subseleção e uma dica de consulta. A dica de consulta é aplicada globalmente. Dicas de consulta não podem ser anexados a instrução de Subseleção.  
  
```  
-- Uses AdventureWorks  
  
CREATE VIEW CustomerView AS  
SELECT CustomerKey, FirstName, LastName FROM ssawPDW..DimCustomer;  
  
SELECT * FROM (  
SELECT COUNT (*) AS a FROM dbo.CustomerView a  
INNER JOIN dbo.FactInternetSales b  
ON ( a.CustomerKey = b.CustomerKey )) AS t  
OPTION (HASH JOIN);  
```  
  
### <a name="g-force-the-join-order-to-match-the-order-in-the-query"></a>G. Forçar a ordem de junção para corresponder à ordem na consulta  
 O exemplo a seguir usa a dica ORDER FORCE para forçar o plano de consulta para usar a ordem de junção especificada pela consulta. Isso melhorará o desempenho em algumas consultas; nem todas as consultas.  
  
```  
-- Uses AdventureWorks  
  
-- Obtain partition numbers, boundary values, boundary value types, and rows per boundary  
-- for the partitions in the ProspectiveBuyer table of the ssawPDW database.  
SELECT sp.partition_number, prv.value AS boundary_value, lower(sty.name) AS boundary_value_type, sp.rows   
FROM sys.tables st JOIN sys.indexes si ON st.object_id = si.object_id AND si.index_id <2  
JOIN sys.partitions sp ON sp.object_id = st.object_id AND sp.index_id = si.index_id  
JOIN sys.partition_schemes ps ON ps.data_space_id = si.data_space_id   
JOIN sys.partition_range_values prv ON prv.function_id = ps.function_id   
JOIN sys.partition_parameters pp ON pp.function_id = ps.function_id   
JOIN sys.types sty ON sty.user_type_id = pp.user_type_id AND prv.boundary_id = sp.partition_number   
WHERE st.object_id = (SELECT object_id FROM sys.objects WHERE name = 'FactResellerSales')   
ORDER BY sp.partition_number  
OPTION ( FORCE ORDER )  
;  
```  
  
### <a name="h-using-externalpushdown"></a>H. Usando EXTERNALPUSHDOWN  
 O exemplo a seguir força a aplicação da cláusula WHERE para o trabalho de MapReduce na tabela externa do Hadoop.  
  
```  
SELECT ID FROM External_Table_AS A   
WHERE ID < 1000000  
OPTION (FORCE EXTERNALPUSHDOWN);  
```  
  
 O exemplo a seguir impede a aplicação da cláusula WHERE para o trabalho de MapReduce na tabela externa do Hadoop. Todas as linhas são retornadas ao PDW onde a cláusula WHERE é aplicada.  
  
```  
SELECT ID FROM External_Table_AS A   
WHERE ID < 10  
OPTION (DISABLE EXTERNALPUSHDOWN);  
```  
  
## <a name="see-also"></a>Consulte também  
 [Dicas de &#40; Transact-SQL &#41;](../../t-sql/queries/hints-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [Mesclar &#40; Transact-SQL &#41;](../../t-sql/statements/merge-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)  
  
  


