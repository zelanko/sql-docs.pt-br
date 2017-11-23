---
title: MAX (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- MAX
- MAX_TSQL
dev_langs: TSQL
helpviewer_keywords:
- MAX function [Transact-SQL]
- values [SQL Server], maximum
- maximum values [SQL Server]
ms.assetid: 9b002b69-ab5e-472d-b12e-dc2fbe35ef42
caps.latest.revision: "38"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 2b6921ee07785edce7f1c19e2eb003bc30d489f6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="max-transact-sql"></a>MAX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna o valor máximo na expressão.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
MAX ( [ ALL | DISTINCT ] expression )  
   OVER ( [ partition_by_clause ] order_by_clause )     
```  
  
## <a name="arguments"></a>Argumentos  
 **ALL**  
 Aplica a função de agregação a todos os valores. ALL é o padrão.  
  
 DISTINCT  
 Especifica que cada valor exclusivo é considerado. DISTINCT não é significativo com MAX e está disponível somente para compatibilidade com ISO.  
  
 *expressão*  
 É uma constante, nome de coluna ou função e qualquer combinação de operadores aritméticos, bit a bit e de cadeia de caracteres. MAX pode ser usado com **numérico**, **caracteres**, **uniqueidentifier**, e **datetime** colunas, mas não com **bits**  colunas. Funções de agregação e subconsultas não são permitidas.  
  
 Para obter mais informações, veja [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 SOBRE **(** [ *partition_by_clause* ] *order_by_clause***)**  
 *partition_by_clause* divide o conjunto de resultados produzido pela cláusula FROM em partições para o qual a função é aplicada. Se não for especificado, a função tratará todas as linhas do conjunto de resultados da consulta como um único grupo. *order_by_clause* determina a ordem lógica na qual a operação é executada. *order_by_clause* é necessário. Para obter mais informações, consulte [a cláusula OVER &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna um valor igual a *expressão*.  
  
## <a name="remarks"></a>Comentários  
 MAX ignora quaisquer valores nulos.  
  
 Para colunas de caracteres, MAX localiza o valor mais alto na sequência de agrupamento.  
  
 MAX é uma função determinística quando usada sem as cláusulas OVER e ORDER BY. É não determinística quando especificada com as cláusulas OVER e ORDER BY. Para obter mais informações, veja [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-simple-example"></a>A. Exemplo simples  
 O exemplo a seguir retorna a taxa de imposto mais alta (máxima) no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql  
SELECT MAX(TaxRate)  
FROM Sales.SalesTaxRate;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 -------------------  
 19.60  
 Warning, null value eliminated from aggregate.  
  
 (1 row(s) affected)  
 ```  
  
### <a name="b-using-the-over-clause"></a>B. Usando a cláusula OVER  
 O exemplo a seguir usa as funções MIN, MAX, AVG e COUNT com a cláusula OVER para fornecer valores agregados para cada departamento no `HumanResources.Department` tabela o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] banco de dados.  
  
```sql  
SELECT DISTINCT Name  
       , MIN(Rate) OVER (PARTITION BY edh.DepartmentID) AS MinSalary  
       , MAX(Rate) OVER (PARTITION BY edh.DepartmentID) AS MaxSalary  
       , AVG(Rate) OVER (PARTITION BY edh.DepartmentID) AS AvgSalary  
       ,COUNT(edh.BusinessEntityID) OVER (PARTITION BY edh.DepartmentID) AS EmployeesPerDept  
FROM HumanResources.EmployeePayHistory AS eph  
JOIN HumanResources.EmployeeDepartmentHistory AS edh  
     ON eph.BusinessEntityID = edh.BusinessEntityID  
JOIN HumanResources.Department AS d  
 ON d.DepartmentID = edh.DepartmentID  
WHERE edh.EndDate IS NULL  
ORDER BY Name;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Name                          MinSalary             MaxSalary             AvgSalary             EmployeesPerDept  
----------------------------- --------------------- --------------------- --------------------- ----------------  
Document Control              10.25                 17.7885               14.3884               5  
Engineering                   32.6923               63.4615               40.1442               6  
Executive                     39.06                 125.50                68.3034               4  
Facilities and Maintenance    9.25                  24.0385               13.0316               7  
Finance                       13.4615               43.2692               23.935                10  
Human Resources               13.9423               27.1394               18.0248               6  
Information Services          27.4038               50.4808               34.1586               10  
Marketing                     13.4615               37.50                 18.4318               11  
Production                    6.50                  84.1346               13.5537               195  
Production Control            8.62                  24.5192               16.7746               8  
Purchasing                    9.86                  30.00                 18.0202               14  
Quality Assurance             10.5769               28.8462               15.4647               6  
Research and Development      40.8654               50.4808               43.6731               4  
Sales                         23.0769               72.1154               29.9719               18  
Shipping and Receiving        9.00                  19.2308               10.8718               6  
Tool Design                   8.62                  29.8462               23.5054               6  
  
 (16 row(s) affected)  
```  
  
### <a name="c-using-max-with-character-data"></a>C. Usando o máximo com dados de caracteres   
O exemplo a seguir retorna o nome do banco de dados que classifica como o último nome em ordem alfabética. O exemplo usa `WHERE database_id < 5`, considerar somente os bancos de dados do sistema.  
```sql   
SELECT MAX(name) FROM sys.databases WHERE database_id < 5;
```
O último banco de dados do sistema `tempdb`.  
  
## <a name="see-also"></a>Consulte também  
 [Funções de agregação &#40; Transact-SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [SOBRE cláusula &#40; Transact-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)  
  
  

