---
title: GROUPING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- GROUPING
- GROUPING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- null values [SQL Server], GROUPING function
- grouping columns
- ROLLUP operator
- GROUP BY clause, GROUPING function
- GROUPING function
- CUBE operator
ms.assetid: 4efa3868-1fc4-4626-8fb1-e863cc03e422
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 513a61c37f0a885bd4f594af062ce6137b84f882
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33052856"
---
# <a name="grouping-transact-sql"></a>GROUPING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Indica se uma expressão de coluna especificada em uma lista GROUP BY é agregada ou não. GROUPING retorna 1 para agregada ou 0 para não agregada no conjunto de resultados. GROUPING pode ser usado apenas na lista SELECT \<select>, nas cláusulas HAVING e ORDER BY, quando GROUP BY é especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
GROUPING ( <column_expression> )  
```  
  
## <a name="arguments"></a>Argumentos  
 \<column_expression>  
 É uma coluna ou uma expressão que contém uma coluna em uma cláusula [GROUP BY](../../t-sql/queries/select-group-by-transact-sql.md).  
  
## <a name="return-types"></a>Tipos de retorno  
 **tinyint**  
  
## <a name="remarks"></a>Remarks  
 GROUPING é usado para distinguir os valores nulos retornados por ROLLUP, CUBE ou GROUPING SETS dos valores nulos padrão. O NULL retornado como resultado de uma operação ROLLUP, CUBE ou GROUPING SETS é um uso especial de NULL. Isto atua como um espaço reservado de coluna no conjunto de resultados e significa tudo.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir agrupa `SalesQuota` e agrega quantias de `SaleYTD` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. A função `GROUPING` é aplicada à coluna `SalesQuota`.  
  
```  
SELECT SalesQuota, SUM(SalesYTD) 'TotalSalesYTD', GROUPING(SalesQuota) AS 'Grouping'  
FROM Sales.SalesPerson  
GROUP BY SalesQuota WITH ROLLUP;  
GO  
```  
  
 O conjunto de resultados mostra dois valores nulos em `SalesQuota`. O primeiro `NULL` representa o grupo de valores nulos desta coluna na tabela. O segundo `NULL` está na linha de resumo somada pela operação ROLLUP. A linha de resumo mostra as quantidades de `TotalSalesYTD` para todos os grupos `SalesQuota` e é indicada por `1` na coluna `Grouping`.  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 SalesQuota     TotalSalesYTD       Grouping  
------------   -----------------   --------  
NULL           1533087.5999          0  
250000.00      33461260.59           0  
300000.00      9299677.9445          0  
NULL           44294026.1344         1  

(4 row(s) affected)
```  
  
## <a name="see-also"></a>Consulte Também  
 [GROUPING_ID &#40;Transact-SQL&#41;](../../t-sql/functions/grouping-id-transact-sql.md)   
 [GROUP BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-group-by-transact-sql.md)  
  
  
