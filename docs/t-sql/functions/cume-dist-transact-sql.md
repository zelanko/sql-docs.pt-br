---
description: CUME_DIST (Transact-SQL)
title: CUME_DIST (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CUME_DIST
- CUME_DIST_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CUME_DIST function
- analytic functions, CUME_DIST
ms.assetid: 491b07f3-9ffd-4cdd-93e5-5abb636fc5ef
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 761e940e04bc0d61c7b78102a9c3cc2a37ff016a
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91115271"
---
# <a name="cume_dist-transact-sql"></a>CUME_DIST (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa função calcula a distribuição cumulativa com um valor em um grupo de valores. Em outras palavras, `CUME_DIST` computa a posição relativa de um valor especificado em um grupo de valores. Supondo a ordenação ascendente, o `CUME_DIST` de um valor na linha _r_ é definido como o número de linhas com valores menores ou iguais ao valor de _r_, dividido pelo número de linhas avaliadas no conjunto de resultados da consulta ou partição. `CUME_DIST` é semelhante à função `PERCENT_RANK`.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
CUME_DIST( )  
    OVER ( [ partition_by_clause ] order_by_clause )  
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
OVER **(** [ _partition\_by\_clause_ ] _order\_by\_clause_)  

A _partition\_by\_clause_ divide o conjunto de resultados produzido pela cláusula FROM em partições às quais a função é aplicada. Se o argumento _partition\_by\_clause_ não tiver sido especificado, `CUME_DIST` tratará todas as linhas do conjunto de resultados da consulta como um único grupo. A _order\_by\_clause_ determina a ordem lógica na qual a operação ocorre. O `CUME_DIST` exige a _order\_by\_clause_. `CUME_DIST` não aceitará a \<rows or range clause> da sintaxe OVER. Para obter mais informações, consulte [Cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md).
  
## <a name="return-types"></a>Tipos de retorno
**float(53)**
  
## <a name="remarks"></a>Comentários  
O `CUME_DIST` retorna um intervalo de valores maior que 0 e menor que ou igual a 1. Valores vinculados são sempre avaliados com o mesmo valor de distribuição cumulativo. O `CUME_DIST` inclui valores NULL por padrão e trata esses valores como os menores valores possíveis.
  
`CUME_DIST` é não determinístico. Para obter mais informações, veja [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir usa a função `CUME_DIST` para calcular o percentil do salário de cada funcionário dentro de um determinado departamento. O `CUME_DIST` retorna um valor que representa a porcentagem de funcionários que tem um salário menor que ou igual ao funcionário atual no mesmo departamento. A função `PERCENT_RANK` calcula a classificação da porcentagem do salário do funcionário dentro de um departamento. Para particionar as linhas do conjunto de resultados por departamento, o exemplo especifica o valor _partition\_by\_clause_. A cláusula ORDER BY da cláusula OVER ordena logicamente as linhas em cada partição. A cláusula ORDER BY da instrução SELECT determina a ordem de exibição do conjunto de resultados.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT Department, LastName, Rate,   
       CUME_DIST () OVER (PARTITION BY Department ORDER BY Rate) AS CumeDist,   
       PERCENT_RANK() OVER (PARTITION BY Department ORDER BY Rate ) AS PctRank  
FROM HumanResources.vEmployeeDepartmentHistory AS edh  
    INNER JOIN HumanResources.EmployeePayHistory AS e    
    ON e.BusinessEntityID = edh.BusinessEntityID  
WHERE Department IN (N'Information Services',N'Document Control')   
ORDER BY Department, Rate DESC;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Department             LastName               Rate                  CumeDist               PctRank  
---------------------- ---------------------- --------------------- ---------------------- ----------------------  
Document Control       Arifin                 17.7885               1                      1  
Document Control       Norred                 16.8269               0.8                    0.5  
Document Control       Kharatishvili          16.8269               0.8                    0.5  
Document Control       Chai                   10.25                 0.4                    0  
Document Control       Berge                  10.25                 0.4                    0  
Information Services   Trenary                50.4808               1                      1  
Information Services   Conroy                 39.6635               0.9                    0.888888888888889  
Information Services   Ajenstat               38.4615               0.8                    0.666666666666667  
Information Services   Wilson                 38.4615               0.8                    0.666666666666667  
Information Services   Sharma                 32.4519               0.6                    0.444444444444444  
Information Services   Connelly               32.4519               0.6                    0.444444444444444  
Information Services   Berg                   27.4038               0.4                    0  
Information Services   Meyyappan              27.4038               0.4                    0  
Information Services   Bacon                  27.4038               0.4                    0  
Information Services   Bueno                  27.4038               0.4                    0  
(15 row(s) affected)  
```  
  
## <a name="see-also"></a>Confira também
[PERCENT_RANK &#40;Transact-SQL&#41;](../../t-sql/functions/percent-rank-transact-sql.md)
  
  
