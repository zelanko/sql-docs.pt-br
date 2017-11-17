---
title: IN (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/29/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 70b186107966791e29ccb76ea9c310724b76e3b6
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="in-transact-sql"></a>IN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Determina se um valor especificado corresponde a qualquer valor em uma subconsulta ou uma lista.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
test_expression [ NOT ] IN   
    ( subquery | expression [ ,...n ]  
    )   
```  
  
## <a name="arguments"></a>Argumentos  
 *test_expression*  
 É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 *subconsulta*  
 É uma subconsulta que tem um conjunto de resultados de uma coluna. Essa coluna deve ter os mesmos dados de tipo como *test_expression*.  
  
 *expressão*[ **,**... *n* ]  
 É uma lista de expressões que testa uma correspondência. Todas as expressões devem ser do mesmo tipo como *test_expression*.  
  
## <a name="result-types"></a>Tipos de resultado  
 **Booliano**  
  
## <a name="result-value"></a>Valor do resultado  
 Se o valor de *test_expression* é igual a qualquer valor retornado por *subconsulta* ou é igual a qualquer *expressão* na lista separada por vírgulas, o valor do resultado for TRUE; Caso contrário, o valor do resultado será FALSE.  
  
 Usar NOT IN nega o *subconsulta* valor ou *expressão*.  
  
> [!CAUTION]  
>  Qualquer valor nulo retornado por *subconsulta* ou *expressão* que são comparados aos *test_expression* usando IN ou NOT IN retornará UNKNOWN. Usar valores nulos junto com IN ou NOT IN pode produzir resultados inesperados.  
  
## <a name="remarks"></a>Comentários  
 Incluir explicitamente um número muito grande de valores (muitos milhares de valores separados por vírgulas) dentro dos parênteses, em uma cláusula IN pode consumir recursos e retornar erros 8623 ou 8632. Para contornar esse problema, armazene os itens na lista em uma tabela e use uma subconsulta SELECT dentro de uma cláusula IN.  
  
 Erro 8623:  
  
 `The query processor ran out of internal resources and could not produce a query plan. This is a rare event and only expected for extremely complex queries or queries that reference a very large number of tables or partitions. Please simplify the query. If you believe you have received this message in error, contact Customer Support Services for more information.`  
  
 Erro 8632:  
  
 `Internal error: An expression services limit has been reached. Please look for potentially complex expressions in your query, and try to simplify them.`  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-comparing-or-and-in"></a>A. Comparando OR e IN  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-in-and-not-in"></a>D. Usando em e não no  
 O exemplo a seguir localiza todas as entradas na `FactInternetSales` correspondentes da tabela `SalesReasonKey` valores no `DimSalesReason` tabela.  
  
```  
-- Uses AdventureWorks  
  
SELECT * FROM FactInternetSalesReason   
WHERE SalesReasonKey   
IN (SELECT SalesReasonKey FROM DimSalesReason);   
```  
  
 O exemplo a seguir localiza todas as entradas na `FactInternetSalesReason` tabela que não correspondem a `SalesReasonKey` valores no `DimSalesReason` tabela.  
  
```  
-- Uses AdventureWorks  
  
SELECT * FROM FactInternetSalesReason   
WHERE SalesReasonKey   
NOT IN (SELECT SalesReasonKey FROM DimSalesReason);  
```  
  
### <a name="e-using-in-with-an-expression-list"></a>E. Usando com uma lista de expressões  
 O exemplo a seguir localiza todas as IDs para os vendedores no `DimEmployee` da tabela de funcionários que têm o primeiro nome que é o `Mike` ou `Michael`.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM DimEmployee  
WHERE FirstName IN ('Mike', 'Michael');  
```  
  
## <a name="see-also"></a>Consulte também  
 [Caso &#40; Transact-SQL &#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [Expressões &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [ONDE &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [Todos os &#40; Transact-SQL &#41;](../../t-sql/language-elements/all-transact-sql.md)   
 [Alguns &#124; QUALQUER &#40; Transact-SQL &#41;](../../t-sql/language-elements/some-any-transact-sql.md)  
  
  




