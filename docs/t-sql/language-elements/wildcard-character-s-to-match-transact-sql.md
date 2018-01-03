---
title: "[] (Curinga – caracteres a serem correspondidos) (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 12/06/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Match
- wildcard
- '[ ]'
- '[_]_TSQL'
dev_langs: TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- '[ ] (wildcard - character(s) to match)'
ms.assetid: 57817576-0bf1-49ed-b05d-fac27e8fed7a
caps.latest.revision: "32"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e6de8f9b9a1ed36135915e5985312a02c02fba6d
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="--wildcard---characters-to-match-transact-sql"></a>\[\] (Curinga - caractere (s) para correspondência) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Corresponde a qualquer caractere único dentro do intervalo especificado ou o conjunto especificado entre colchetes `[ ]`. Esses caracteres curinga podem ser usados em comparações de cadeia de caracteres que envolvem a correspondência de padrões, como `LIKE` e `PATINDEX`.  
  
## <a name="examples"></a>Exemplos  
### <a name="a-simple-example"></a>R: exemplo simples de   
O exemplo a seguir retorna os nomes dos que começam com a letra `m`. `[n-z]`Especifica que a segunda letra deve ser em algum lugar no intervalo de `n` para `z`. O caractere curinga porcentagem `%` permite caracteres todos ou nenhum, começando com o caractere de 3. O `model` e `msdb` bancos de dados atendem esse critério. O `master` banco de dados não funciona e é excluído do conjunto de resultados.
 
```sql
SELECT name FROM sys.databases
WHERE name LIKE 'm[n-z]%';
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]  

```
name
-----
model
msdb
```   
 Você pode ter outros bancos de dados qualificados instalados.


### <a name="b-more-complex-example"></a>B: exemplo mais complexo   
 O exemplo a seguir usa o operador [] para encontrar as IDs e os nomes de todos os funcionários da [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] que possuem endereços com um código postal de quatro dígitos.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT e.BusinessEntityID, p.FirstName, p.LastName, a.PostalCode  
FROM HumanResources.Employee AS e  
INNER JOIN Person.Person AS p ON e.BusinessEntityID = p.BusinessEntityID  
INNER JOIN Person.BusinessEntityAddress AS ea ON e.BusinessEntityID = ea.BusinessEntityID  
INNER JOIN Person.Address AS a ON a.AddressID = ea.AddressID  
WHERE a.PostalCode LIKE '[0-9][0-9][0-9][0-9]';  
```  
  
 Este é o conjunto de resultados:  
  
```  
EmployeeID      FirstName      LastName      PostalCode  
----------      ---------      ---------     ----------  
290             Lynn           Tsoflias      3000  
```  



  
## <a name="see-also"></a>Consulte Também  
 [COMO &#40; Transact-SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40; Transact-SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [% &#40; Curinga – caracteres &#40; s &#41; a correspondência &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
 [&#91; ^ &#93; &#40; Curinga – caracteres &#40; s &#41; Para não coincidir &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
 [\_&#40; Curinga – corresponde a um caractere &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
    
  
