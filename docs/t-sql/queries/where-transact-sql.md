---
title: ONDE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- WHERE_TSQL
- WHERE
dev_langs:
- TSQL
helpviewer_keywords:
- retrieving rows
- clauses [SQL Server], WHERE
- WHERE clause, about WHERE clause
- row retrieval [SQL Server], WHERE clause
- WHERE clause
ms.assetid: a8430421-7bce-4fab-a2d2-56c00a3c6fa4
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5835510f37f52d57d2c23918a30dde10e7496a5d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="where-transact-sql"></a>WHERE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Especifica o critério de pesquisa para as linhas retornadas pela consulta.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
[ WHERE <search_condition> ]  
```  
  
## <a name="arguments"></a>Argumentos  
\<*search_condition* > define a condição a ser atendida para as linhas a serem retornadas. Não há nenhum limite para o número de predicados que podem ser incluídos em um critério de pesquisa. Para obter mais informações sobre critérios de pesquisa e predicados, consulte [critério de pesquisa &#40; Transact-SQL &#41; ](../../t-sql/queries/search-condition-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir mostram como usar algumas condições de pesquisa comuns na cláusula `WHERE`.  
  
### <a name="a-finding-a-row-by-using-a-simple-equality"></a>A. Localizando uma linha com o uso de uma igualdade simples  
  
```  
USE AdventureWorks2012  
GO  
SELECT ProductID, Name  
FROM Production.Product  
WHERE Name = 'Blade' ;  
GO  
```  
  
### <a name="b-finding-rows-that-contain-a-value-as-a-part-of-a-string"></a>B. Localizando linhas que contêm um valor como parte de uma cadeia de caracteres  
  
```  
SELECT ProductID, Name, Color  
FROM Production.Product  
WHERE Name LIKE ('%Frame%');  
GO  
```  
  
### <a name="c-finding-rows-by-using-a-comparison-operator"></a>C. Localizando linhas com o uso de um operador de comparação  
  
```  
SELECT ProductID, Name  
FROM Production.Product  
WHERE ProductID <= 12 ;  
GO  
```  
  
### <a name="d-finding-rows-that-meet-any-of-three-conditions"></a>D. Localizando linhas que atendem a qualquer uma de três condições  
  
```  
SELECT ProductID, Name  
FROM Production.Product  
WHERE ProductID = 2  
OR ProductID = 4   
OR Name = 'Spokes' ;  
GO  
```  
  
### <a name="e-finding-rows-that-must-meet-several-conditions"></a>E. Localizando linhas que devem atender a várias condições  
  
```  
SELECT ProductID, Name, Color  
FROM Production.Product  
WHERE Name LIKE ('%Frame%')  
AND Name LIKE ('HL%')  
AND Color = 'Red' ;  
GO  
```  
  
### <a name="f-finding-rows-that-are-in-a-list-of-values"></a>F. Localizando linhas que estão em uma lista de valores  
  
```  
SELECT ProductID, Name, Color  
FROM Production.Product  
WHERE Name IN ('Blade', 'Crown Race', 'Spokes');  
GO  
```  
  
### <a name="g-finding-rows-that-have-a-value-between-two-values"></a>G. Localizando linhas que têm um valor entre dois valores  
  
```  
SELECT ProductID, Name, Color  
FROM Production.Product  
WHERE ProductID BETWEEN 725 AND 734;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Os exemplos a seguir mostram como usar algumas condições de pesquisa comuns na cláusula `WHERE`.  
  
### <a name="h-finding-a-row-by-using-a-simple-equality"></a>H. Localizando uma linha com o uso de uma igualdade simples  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName = 'Smith' ;  
```  
  
### <a name="i-finding-rows-that-contain-a-value-as-part-of-a-string"></a>I. Localizando linhas que contêm um valor como parte de uma cadeia de caracteres  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName LIKE ('%Smi%');  
```  
  
### <a name="j-finding-rows-by-using-a-comparison-operator"></a>J. Localizando linhas com o uso de um operador de comparação  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE EmployeeKey  <= 500;  
```  
  
### <a name="k-finding-rows-that-meet-any-of-three-conditions"></a>K. Localizando linhas que atendem a qualquer uma de três condições  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE EmployeeKey = 1 OR EmployeeKey = 8 OR EmployeeKey = 12;  
```  
  
### <a name="l-finding-rows-that-must-meet-several-conditions"></a>L. Localizando linhas que devem atender a várias condições  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE EmployeeKey <= 500 AND LastName LIKE '%Smi%' AND FirstName LIKE '%A%';  
```  
  
### <a name="m-finding-rows-that-are-in-a-list-of-values"></a>M. Localizando linhas que estão em uma lista de valores  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName IN ('Smith', 'Godfrey', 'Johnson');  
```  
  
### <a name="n-finding-rows-that-have-a-value-between-two-values"></a>N. Localizando linhas que têm um valor entre dois valores  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE EmployeeKey Between 100 AND 200;  
```  
  
## <a name="see-also"></a>Consulte também  
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [Predicados &#40; Transact-SQL &#41;](~/t-sql/queries/predicates.md)   
 [Critério de pesquisa &#40; Transact-SQL &#41;](../../t-sql/queries/search-condition-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)  
  
  



