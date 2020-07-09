---
title: IN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IN_TSQL
- IN
dev_langs:
- TSQL
helpviewer_keywords:
- values [SQL Server], matching
- NOT IN keyword
- 8623 (Database Engine error)
- matching values in subquery or list [SQL Server]
- IN keyword
- 8632 (Database Engine error)
ms.assetid: 4419de73-96b1-4dfe-8500-f4507915db04
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 728d11420c1a91e581fa153020174f2d4339311f
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86007357"
---
# <a name="in-transact-sql"></a>IN (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Determina se um valor especificado corresponde a qualquer valor em uma subconsulta ou uma lista.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
test_expression [ NOT ] IN   
    ( subquery | expression [ ,...n ]  
    )   
```  
  
## <a name="arguments"></a>Argumentos  
 *test_expression*  
 É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md) válida.  
  
 *subquery*  
 É uma subconsulta que tem um conjunto de resultados de uma coluna. Essa coluna deve ter o mesmo tipo de dados que *test_expression*.  
  
 *expression*[ **,** ... *n* ]  
 É uma lista de expressões que testa uma correspondência. Todas as expressões devem ser do mesmo tipo que *test_expression*.  
  
## <a name="result-types"></a>Tipos de resultado  
 **Booliano**  
  
## <a name="result-value"></a>Valor do resultado  
 Se o valor de *test_expression* for igual a qualquer valor retornado por *subquery* ou igual a qualquer *expression* da lista separada por vírgula, o valor do resultado será TRUE, caso contrário, será FALSE.  
  
 O uso de NOT IN nega o valor de *subquery* ou *expression*.  
  
> [!CAUTION]  
>  Os valores nulos retornados por *subquery* ou *expression* que são comparados com *test_expression* usando IN ou NOT IN retornam UNKNOWN. Usar valores nulos junto com IN ou NOT IN pode produzir resultados inesperados.  
  
## <a name="remarks"></a>Comentários  
 A inclusão explícita de um número muito grande de valores (muitos milhares de valores separados por vírgula) dentro dos parênteses, em uma cláusula IN, pode consumir recursos e retornar os erros 8623 ou 8632. Para resolver esse problema, armazene os itens na lista IN em uma tabela e use uma subconsulta SELECT dentro de uma cláusula IN.  
  
 Erro 8623:  
  
 `The query processor ran out of internal resources and could not produce a query plan. This is a rare event and only expected for extremely complex queries or queries that reference a very large number of tables or partitions. Please simplify the query. If you believe you have received this message in error, contact Customer Support Services for more information.`  
  
 Erro 8632:  
  
 `Internal error: An expression services limit has been reached. Please look for potentially complex expressions in your query, and try to simplify them.`  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-comparing-or-and-in"></a>a. Comparando OR e IN  
 O exemplo a seguir seleciona uma lista de nomes de funcionários que são engenheiros de design, designers de ferramentas ou assistentes de marketing.  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, e.JobTitle  
FROM Person.Person AS p  
JOIN HumanResources.Employee AS e  
    ON p.BusinessEntityID = e.BusinessEntityID  
WHERE e.JobTitle = 'Design Engineer'   
   OR e.JobTitle = 'Tool Designer'   
   OR e.JobTitle = 'Marketing Assistant';  
GO  
```  
  
 Entretanto, você recupera os mesmos resultados usando IN.  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, e.JobTitle  
FROM Person.Person AS p  
JOIN HumanResources.Employee AS e  
    ON p.BusinessEntityID = e.BusinessEntityID  
WHERE e.JobTitle IN ('Design Engineer', 'Tool Designer', 'Marketing Assistant');  
GO  
```  
  
 Aqui está o conjunto de resultados das duas consultas.  
  
```  
FirstName   LastName      Title  
---------   ---------   ---------------------  
Sharon      Salavaria   Design Engineer                                     
Gail        Erickson    Design Engineer                                     
Jossef      Goldberg    Design Engineer                                     
Janice      Galvin      Tool Designer                                       
Thierry     D'Hers      Tool Designer                                       
Wanida      Benshoof    Marketing Assistant                                 
Kevin       Brown       Marketing Assistant                                 
Mary        Dempsey     Marketing Assistant                                 
  
(8 row(s) affected)  
```  
  
### <a name="b-using-in-with-a-subquery"></a>B. Usando IN com uma subconsulta  
 O exemplo a seguir encontra todas as IDs para os vendedores na tabela `SalesPerson` para funcionários com uma cota de venda maior que $ 250.000 por ano, e seleciona na tabela `Employee` os nomes de todos os funcionários em que `EmployeeID` corresponde aos resultados da subconsulta `SELECT`.  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName  
FROM Person.Person AS p  
    JOIN Sales.SalesPerson AS sp  
    ON p.BusinessEntityID = sp.BusinessEntityID  
WHERE p.BusinessEntityID IN  
   (SELECT BusinessEntityID  
   FROM Sales.SalesPerson  
   WHERE SalesQuota > 250000);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
FirstName   LastName                                             
---------   --------   
Tsvi         Reiter                                              
Michael      Blythe                                              
Tete         Mensa-Annan                                         
  
(3 row(s) affected)  
```  
  
### <a name="c-using-not-in-with-a-subquery"></a>C. Usando NOT IN com uma subconsulta  
 O exemplo a seguir localiza os vendedores que não têm uma cota maior que US$ 250.000. `NOT IN` localiza os vendedores que não correspondem aos itens da lista de valores.  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName  
FROM Person.Person AS p  
    JOIN Sales.SalesPerson AS sp  
    ON p.BusinessEntityID = sp.BusinessEntityID  
WHERE p.BusinessEntityID NOT IN  
   (SELECT BusinessEntityID  
   FROM Sales.SalesPerson  
   WHERE SalesQuota > 250000);  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-in-and-not-in"></a>D. Usando IN e NOT IN  
 O exemplo a seguir localiza todas as entradas na tabela `FactInternetSales` correspondentes aos valores `SalesReasonKey` na tabela `DimSalesReason`.  
  
```  
-- Uses AdventureWorks  
  
SELECT * FROM FactInternetSalesReason   
WHERE SalesReasonKey   
IN (SELECT SalesReasonKey FROM DimSalesReason);   
```  
  
 O exemplo a seguir localiza todas as entradas na tabela `FactInternetSalesReason` não correspondentes aos valores `SalesReasonKey` na tabela `DimSalesReason`.  
  
```  
-- Uses AdventureWorks  
  
SELECT * FROM FactInternetSalesReason   
WHERE SalesReasonKey   
NOT IN (SELECT SalesReasonKey FROM DimSalesReason);  
```  
  
### <a name="e-using-in-with-an-expression-list"></a>E. Usando IN com uma lista de expressões  
 O exemplo a seguir localiza todas as IDs para os vendedores na tabela `DimEmployee` de funcionários que têm o nome `Mike` ou `Michael`.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM DimEmployee  
WHERE FirstName IN ('Mike', 'Michael');  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [ALL &#40;Transact-SQL&#41;](../../t-sql/language-elements/all-transact-sql.md)   
 [SOME &#124; ANY &#40;Transact-SQL&#41;](../../t-sql/language-elements/some-any-transact-sql.md)  
  
  



