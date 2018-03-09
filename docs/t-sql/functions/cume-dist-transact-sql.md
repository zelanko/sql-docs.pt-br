---
title: CUME_DIST (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: dadae05fa8556b403c6cba436647203b30452559
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="cumedist-transact-sql"></a>CUME_DIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

Calcula a distribuição cumulativa de um valor em um grupo de valores no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ou seja, CUME_DIST computa a posição relativa de um valor especificado em um grupo de valores. Para uma linha *r*, assumindo a ordenação crescente, CUME_DIST de *r* é o número de linhas com valores menores ou iguais ao valor de *r*, dividido pelo número de linhas avaliada no conjunto de resultados de consulta ou partição. CUME_DIST é semelhante à função PERCENT_RANK.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CUME_DIST( )  
    OVER ( [ partition_by_clause ] order_by_clause )  
  
```  
  
## <a name="arguments"></a>Argumentos  
SOBRE **(** [ *partition_by_clause* ] *order_by_clause***)**  
*partition_by_clause* divide o conjunto de resultados produzido pela cláusula FROM em partições para o qual a função é aplicada. Se não for especificado, a função tratará todas as linhas do conjunto de resultados da consulta como um único grupo. *order_by_clause* determina a ordem lógica na qual a operação é executada. *order_by_clause* é necessário. O \<cláusula rows ou range > da OVER sintaxe não pode ser especificada em uma função CUME_DIST. Para obter mais informações, consulte [a cláusula OVER &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).
  
## <a name="return-types"></a>Tipos de retorno
**float(53)**
  
## <a name="remarks"></a>Comentários  
O intervalo de valores retornados por CUME_DIST é maior que 0 e menor ou igual a 1. Valores vinculados são sempre avaliados com o mesmo valor de distribuição cumulativo. Por padrão, valores NULL são incluídos e tratados como os menores valores possíveis.
  
CUME_DIST é não determinística. Para obter mais informações, veja [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir usa a função CUME_DIST para computar o percentil do salário de cada funcionário dentro de um determinado departamento. O valor retornado pela função CUME_DIST representa a porcentagem de funcionários que têm um salário menor ou igual ao funcionário atual no mesmo departamento. A função PERCENT_RANK computa a classificação da porcentagem do salário do funcionário dentro de um departamento. A cláusula PARTITION BY é especificada para particionar as linhas no conjunto de resultados por departamento. A cláusula ORDER BY na cláusula OVER ordena logicamente as linhas em cada partição. A cláusula ORDER BY na instrução SELECT determina a ordem de exibição do conjunto de resultados.
  
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
  
```sql
  
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
  
## <a name="see-also"></a>Consulte também
[PERCENT_RANK &#40; Transact-SQL &#41;](../../t-sql/functions/percent-rank-transact-sql.md)
  
  
