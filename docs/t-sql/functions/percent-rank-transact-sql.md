---
title: PERCENT_RANK (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2015
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PERCENT_RANK_TSQL
- PERCENT_RANK
dev_langs:
- TSQL
helpviewer_keywords:
- PERCENT_RANK function
- analytic functions, PERCENT_RANK
ms.assetid: e361c2d4-c01f-4da4-8e89-1ddc724a2629
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9289c279efcf9d3989bc6fb09c8d37e251d3abc2
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37997534"
---
# <a name="percentrank-transact-sql"></a>PERCENT_RANK (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

  Calcula a classificação relativa de uma linha dentro de um grupo de linhas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Use PERCENT_RANK para avaliar a posição relativa de um valor dentro de um conjunto de resultados de consulta ou partição. PERCENT_RANK é semelhante à função CUME_DIST.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
PERCENT_RANK( )  
    OVER ( [ partition_by_clause ] order_by_clause )  
  
```  
  
## <a name="arguments"></a>Argumentos  
 OVER **(** [ *partition_by_clause* ] *order_by_clause***)**  
 *partition_by_clause* divide o conjunto de resultados produzido pela cláusula FROM em partições às quais a função é aplicada. Se não for especificado, a função tratará todas as linhas do conjunto de resultados da consulta como um único grupo. *order_by_clause* determina a ordem lógica na qual a operação é executada. *order_by_clause* é obrigatória. A \<cláusula rows ou range> da sintaxe OVER não pode ser especificada em uma função PERCENT_RANK.  Para obter mais informações, consulte [Cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Tipos de retorno  
 **float(53)**  
  
## <a name="general-remarks"></a>Comentários gerais  
 O intervalo de valores retornados por PERCENT_RANK é maior que 0 e menor ou igual a 1. A primeira linha de qualquer conjunto tem um PERCENT_RANK de 0. Por padrão, valores NULL são incluídos e tratados como os menores valores possíveis.  
  
 PERCENT_RANK é não determinística. Para obter mais informações, veja [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa a função CUME_DIST para computar o percentil do salário de cada funcionário dentro de um determinado departamento. O valor retornado pela função CUME_DIST representa a porcentagem de funcionários que têm um salário menor ou igual ao funcionário atual no mesmo departamento. A função PERCENT_RANK computa a classificação do salário do funcionário dentro de um departamento como uma porcentagem. A cláusula PARTITION BY é especificada para particionar as linhas no conjunto de resultados por departamento. A cláusula ORDER BY na cláusula OVER ordena as linhas em cada partição. A cláusula ORDER BY na instrução SELECT classifica as linhas em todo o conjunto de resultados.  
  
```  
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
  
## <a name="see-also"></a>Consulte Também  
 [CUME_DIST &#40;Transact-SQL&#41;](../../t-sql/functions/cume-dist-transact-sql.md)  
  
  
