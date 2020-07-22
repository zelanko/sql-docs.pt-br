---
title: WHERE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 98638f23d0216bb100d34d180fce91358724bf56
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554411"
---
# <a name="where-transact-sql"></a>WHERE (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Especifica o critério de pesquisa para as linhas retornadas pela consulta.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
[ WHERE <search_condition> ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
\< *search_condition* > define a condição que deverá ser atendida para as linhas que retornarão. Não há nenhum limite para o número de predicados que podem ser incluídos em um critério de pesquisa. Para obter mais informações sobre critérios de pesquisa e predicados, consulte [Critério de pesquisa &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir mostram como usar algumas condições de pesquisa comuns na cláusula `WHERE`.  
  
### <a name="a-finding-a-row-by-using-a-simple-equality"></a>a. Localizando uma linha com o uso de uma igualdade simples  
  
```  
-- Uses AdventureWorksDW  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName = 'Smith' ;  
```  
  
### <a name="b-finding-rows-that-contain-a-value-as-part-of-a-string"></a>B. Localizando linhas que contêm um valor como parte de uma cadeia de caracteres  
  
```  
-- Uses AdventureWorksDW  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName LIKE ('%Smi%');  
```  
  
### <a name="c-finding-rows-by-using-a-comparison-operator"></a>C. Localizando linhas com o uso de um operador de comparação  
  
```  
-- Uses AdventureWorksDW  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE EmployeeKey  <= 500;  
```  
  
### <a name="d-finding-rows-that-meet-any-of-three-conditions"></a>D. Localizando linhas que atendem a qualquer uma de três condições  
  
```  
-- Uses AdventureWorksDW  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE EmployeeKey = 1 OR EmployeeKey = 8 OR EmployeeKey = 12;  
```  
  
### <a name="e-finding-rows-that-must-meet-several-conditions"></a>E. Localizando linhas que devem atender a várias condições  
  
```  
-- Uses AdventureWorksDW  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE EmployeeKey <= 500 AND LastName LIKE '%Smi%' AND FirstName LIKE '%A%';  
```  
  
### <a name="f-finding-rows-that-are-in-a-list-of-values"></a>F. Localizando linhas que estão em uma lista de valores  
  
```  
-- Uses AdventureWorksDW  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName IN ('Smith', 'Godfrey', 'Johnson');  
```  
  
### <a name="g-finding-rows-that-have-a-value-between-two-values"></a>G. Localizando linhas que têm um valor entre dois valores  
  
```  
-- Uses AdventureWorksDW  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE EmployeeKey Between 100 AND 200;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [Predicados &#40;Transact-SQL&#41;](~/t-sql/queries/predicates.md)   
 [Critério de pesquisa &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)  
  
  


